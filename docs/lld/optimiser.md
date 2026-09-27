# LLD — Basket optimiser

Package `packages/optimiser` (`@mandi/optimiser`), pure TypeScript with no I/O. Decision record: [ADR-0006](../adr/0006-basket-optimiser-by-exact-enumeration-over-store-subsets.md).

## Inputs

```ts
type Paise = number;
interface OptimiserInput {
  items: { productId: string; quantity: number; allowedStores?: string[]; fixedStore?: string }[];
  offers: { productId: string; storeId: string; storeProductId: string; unitPrice: Paise; inStock: boolean }[];
  stores: { storeId: string; tier: 'A' | 'B' | 'C'; etaMin: number; minOrder?: Paise }[];
  feeRules: { id: string; storeId: string; kind: 'delivery'|'handling'|'small_cart'|'surge'|'platform';
              minSubtotal?: Paise; maxSubtotal?: Paise; amount: Paise; waivedByMembership?: string }[];
  memberships: string[];                // e.g. ['zepto_pass']
  tapCost: { perTierCStore: Paise };    // default 1500 (₹15) — friction threshold from the PRD
}
```

Brand rule `same_grade` is resolved before the optimiser runs: the catalog expands such items into a set of acceptable `productId`s, and the optimiser picks the cheapest acceptable offer.

## Algorithm

1. Let `S` = stores with at least one in-stock offer for the basket (N ≤ 8).
2. For every non-empty subset `T ⊆ S` (≤ 255):
   1. For each item, pick the cheapest in-stock offer among stores in `T` that the item allows. If an item has no offer in `T`, the subset is infeasible.
   2. Group lines by store; compute each store's subtotal.
   3. For each store, add every fee rule whose subtotal band matches and that the user's memberships do not waive. If a store's subtotal is under its `minOrder`, the subset is infeasible.
   4. `total(T) = Σ subtotals + Σ fees`; `taps(T) = 2 if any tier A store else 0` + `1 per tier C store` + `1 per tier B store`; `score(T) = total(T) + tapCost × (#tier C stores)`.
3. **Cheapest** = min `total`. **Fewest taps** = min `score`. **Single store** = min `total` among `|T| = 1`. Ties break on fewer stores, then lower max ETA.
4. **Saving** is reported against the best single-store total, never against MRP.
5. Output lists each plan's legs, lines, fees with the `rule_id`s used, and an `inputHash` so the exact plan can be reproduced.

Complexity: 255 subsets × 30 items × 8 stores ≈ 61k operations; well under 5 ms in Node.

## Edge cases to test

- An item only one store carries forces that store into every feasible subset.
- A small-cart fee that makes a two-store split worse than one store (the "Cheapest shelf price" trap in the design).
- Membership waiving delivery fees (Zepto Pass).
- All stores out of stock for an item: plan returns the item under `unavailable[]` instead of failing.
- Quantity changes crossing a fee band.

## Tests

Property tests (fast-check): total equals the sum of legs; no plan contains an out-of-stock line; cheapest ≤ every other plan's total. Golden tests: 30 hand-checked baskets including the PRD examples (₹393 split vs ₹412 single vs ₹429 three-store).
