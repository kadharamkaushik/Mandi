# LLD — Store connectors

Package `packages/connectors` (`@mandi/connectors`). Decision record: [ADR-0007](../adr/0007-tiered-store-connectors.md).

## Interface

```ts
interface StoreConnector {
  readonly storeId: StoreId;
  capabilities(link?: StoreLink): Capabilities;          // tier, canSearch, canOrder, canTrack
  search(q: SearchQuery, ctx: Ctx): Promise<StoreProduct[]>;
  offers(skus: string[], ctx: Ctx): Promise<Offer[]>;    // price, stock, pack, observedAt
  fees(ctx: Ctx): Promise<FeeRule[]>;
  buildCart?(lines: CartLine[], ctx: UserCtx): Promise<CartSnapshot>;       // tier A/B
  placeOrder?(cart: CartSnapshot, ctx: UserCtx, idem: string): Promise<PlacedOrder>; // tier A
  orderStatus?(ref: string, ctx: UserCtx): Promise<OrderStatus>;
  orderHistory?(since: Date, ctx: UserCtx): Promise<PastOrder[]>;
  deepLink(target: { storeProduct?: StoreProduct; search?: string }): HandoffLink; // tier C
}
```

`Ctx` carries pincode cluster, trace context and a budget (timeout, retries). `UserCtx` adds the decrypted store token, loaded per call and never cached in memory beyond the request.

## Zepto (tier A)

- Transport: official MCP server `https://mcp.zepto.co.in/mcp` via `@modelcontextprotocol/sdk` streamable HTTP client, one short-lived client per request.
- Auth: OAuth 2.1 with PKCE; user verifies phone OTP on Zepto's page. Redirect URI `https://api.mandi.app/v1/oauth/zepto/callback` must be allowlisted by Zepto (raise an issue on github.com/zeptonow/mcp with the production domain).
- Tool mapping: discover tool names with `listTools()` at startup and map them in `zepto.tools.ts`; fail the health check if an expected tool disappears. Map: product search → `search`/`offers`; cart add/update/remove → `buildCart`; place order → `placeOrder`; order history → `orderHistory`/`orderStatus`.
- Payment: the user's Zepto payment method (UPI, card, Zepto Cash, UPI Reserve Pay, COD). Mandi passes no payment data.
- Unattended (pre-approved) checkout is not supported by Zepto; every order follows an explicit user confirm.
- Limits: unknown; start with 2 concurrent calls per user and 20 rps overall with a circuit breaker (opossum). On breaker open, capability drops to tier C.

## Instamart (tier A behind flag)

- Official MCP `https://mcp.swiggy.com/im`. Production use needs Swiggy Builders Club approval; the README currently says COD only and warns against using the app and MCP at the same session. Keep `instamart_tier_a` off until written approval; until then Instamart is tier C with prices from feeds.

## Feeds (prices for tier C stores)

- `FeedProvider` interface with one implementation per contracted source (licensed data vendor, affiliate product feed, or partner feed). Output is normalised `Offer` and `FeeRule` rows tagged with `source`.
- No scraping of logged-in sessions and no unofficial wrappers (ADR-0007). The legal route per store is an open question in the PRD and gates MND-023.

## Deep links (tier C)

- Per store, a `HandoffLink = { appUrl, webUrl, searchFallback }`. Prefer a verified product URL (universal link / app link) that the store app opens; fall back to the store's search URL with the product title; last resort is copying the list.
- A nightly job (MND-024) opens a sample of links on emulators and records which patterns still open the right screen; broken patterns switch to search fallback automatically.

## Security

Tokens are envelope-encrypted: a KMS data key per user encrypts the token (AES-256-GCM); only the data key ciphertext is stored with the link. Decryption happens in the API/worker process for the duration of one call. Tokens never appear in logs (pino redaction paths) or traces.

## Fakes

`FakeStoreConnector` implements every method from fixture files, supports latency and failure injection, and backs local dev, integration tests and mobile UI tests.
