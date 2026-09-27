# LLD — Public API (v1)

Base URL `https://api.mandi.app/v1`. JSON over HTTPS, TLS 1.3. The contract lives in [`packages/contracts/openapi.yaml`](../../packages/contracts/openapi.yaml); this page explains the conventions and lists the endpoints the spec must contain.

## Conventions

- **Auth**: `Authorization: Bearer <access JWT>` (EdDSA, 15-minute TTL). Refresh tokens are opaque, 30-day, rotate on every use; reuse of an old refresh token revokes the session family.
- **Idempotency**: every `POST` that creates or orders takes `Idempotency-Key` (UUID). Same key + same body within 24 h returns the stored response; same key + different body returns `409 idempotency_conflict`.
- **Errors**: RFC 9457 problem details: `{ "type", "title", "status", "code", "detail", "fields"? }`. `code` is stable and machine-readable (e.g. `otp_invalid`, `store_link_expired`, `plan_stale`, `price_changed`).
- **Money**: integers in paise plus ISO currency `INR`. Never floats.
- **Pagination**: cursor-based (`?cursor=&limit=`, max 50); responses carry `next_cursor`.
- **Versioning**: breaking changes go to `/v2`; additive fields are allowed in v1 and clients must ignore unknown fields.
- **Rate limits**: per user and per IP in Valkey; `429` with `Retry-After`.
- **Tracing**: clients send `traceparent`; every response echoes `x-request-id`.

## Endpoints

| Method and path | Purpose | PRD |
| --- | --- | --- |
| `POST /auth/otp` | Send OTP to a phone number | F1 |
| `POST /auth/otp/verify` | Verify OTP; returns access + refresh tokens and whether the user is new | F1 |
| `POST /auth/refresh` | Rotate refresh token | F10 |
| `POST /auth/logout` | Revoke current session | F8 |
| `GET /me` · `PATCH /me` | Profile | F8 |
| `DELETE /me` | Request account deletion (30-day hard delete) | F8 |
| `POST /me/export` | Queue a data export; emailed/downloadable link | F8 |
| `GET/PUT /me/consents` | Consent ledger per purpose | F8 |
| `GET/POST /addresses` · `PATCH/DELETE /addresses/{id}` | Addresses | F1, F8 |
| `GET /addresses/{id}/serviceability` | Stores serving the address with ETA | F1 |
| `GET /stores` | Stores with tier and link status for this user | F1, F8 |
| `POST /store-links/{storeId}/start` | Begin OAuth; returns `authorize_url` | F1 |
| `GET /oauth/{storeId}/callback` | OAuth redirect target (browser); completes link | F1 |
| `DELETE /store-links/{storeId}` | Unlink | F8 |
| `POST /usuals/import` | Import usuals from linked store history (async job) | F1 |
| `GET /usuals` · `POST /usuals` · `PATCH/DELETE /usuals/{id}` | Usuals CRUD with rules and cadence | F2 |
| `POST /usuals/pause` | Pause a date range | F2 |
| `GET /search?q=&filters=` | Merged product search across stores | F3 |
| `GET /products/{id}` | Product with nutrition, grade and every store offer | F3, F7 |
| `GET /products/{id}/swaps` | Healthier alternatives at same or lower price | F7 |
| `GET /baskets/current` | Current basket (built from due usuals + adds) | F4 |
| `POST /baskets/current/items` · `PATCH/DELETE /baskets/current/items/{productId}` | Edit basket | F4 |
| `POST /baskets/current/plans` | Compute plans (cheapest, fewest taps, single store) | F4 |
| `POST /baskets/current/checkout` | Check out a plan: re-check, place tier A, return tier C steps | F5 |
| `GET /orders` · `GET /orders/{id}` | Orders and status | F6 |
| `POST /orders/{id}/confirm` | User confirms a tier C order (amount paid) | F6 |
| `POST /orders/{id}/report-issue` | Missing or substituted items | F6 |
| `GET /health-profile` · `PUT /health-profile` | Goals, diet, avoid-list | F1, F7 |
| `GET /insights?month=` | Spend, savings, basket health trends | F7 (P1) |
| `POST /devices` · `DELETE /devices/{id}` | Register push token | F9 |

## Key payloads

`POST /baskets/current/plans` response (abridged):

```json
{
  "basket_id": "0192…",
  "computed_at": "2026-10-12T08:30:00Z",
  "expires_at": "2026-10-12T08:40:00Z",
  "plans": [
    {
      "id": "0192…",
      "kind": "cheapest",
      "total": { "amount": 39300, "currency": "INR" },
      "saving_vs_best_single_store": { "amount": 1900, "currency": "INR" },
      "taps": 4,
      "legs": [
        { "store_id": "blinkit", "tier": "C", "subtotal": {"amount": 19200}, "fees": [], "eta_min": 10,
          "lines": [ { "product_id": "…", "store_product_id": "…", "quantity": 2, "unit_price": {"amount": 5600} } ] },
        { "store_id": "zepto", "tier": "A", "subtotal": {"amount": 19200},
          "fees": [ { "kind": "handling", "amount": {"amount": 900}, "rule_id": "…" } ], "eta_min": 8, "lines": [] }
      ],
      "health": { "grade": "A", "a_share": 0.6 }
    }
  ]
}
```

`POST /baskets/current/checkout` response:

```json
{
  "orders": [ { "id": "…", "store_id": "zepto", "tier": "A", "status": "placed", "store_order_ref": "ZP-…" } ],
  "handoffs": [
    { "order_id": "…", "store_id": "blinkit", "tier": "C",
      "steps": [ { "product_id": "…", "title": "Amul Taaza Toned Milk 1 L", "quantity": 2,
                   "open_url": "https://…", "fallback_search": "amul taaza toned milk 1 l" } ] }
  ],
  "changes": []
}
```

If any price moved more than ₹5 or an item went out of stock since the plan, the endpoint returns `409 price_changed` with `changes[]` and places nothing.
