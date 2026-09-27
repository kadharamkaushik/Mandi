---
id: MND-033
title: "Checkout router: re-check, tier A orders, tier C hand-off steps"
epic: CORE
prd: F5
status: todo
owner: agent
size: L
depends_on: [MND-032, MND-021, MND-024]
---

# MND-033 — Checkout router: re-check, tier A orders, tier C hand-off steps

**Why:** One confirm tap fans out into direct orders for tier A stores and a hand-off checklist for tier C stores. Mandi never touches payment.

Epic `CORE` · PRD F5 · Size L (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-032
- MND-021
- MND-024

## Read first

- [docs/hld.md#3-checkout-tiers](../../docs/hld.md#3-checkout-tiers)
- [docs/lld/api.md#key-payloads](../../docs/lld/api.md#key-payloads)
- [docs/adr/0004-mandi-never-holds-customer-money.md](../../docs/adr/0004-mandi-never-holds-customer-money.md)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] POST /baskets/current/checkout with Idempotency-Key: re-check prices and stock; return 409 price_changed with changes if any line moved > ₹5 or went out of stock.
- [ ] Tier A: buildCart + placeOrder per store in parallel; create orders rows; partial failure leaves successful orders and reports the failed store as tier C fallback.
- [ ] Tier C: create pending orders and hand-off steps from deepLink().
- [ ] Emit order.placed events through the outbox.

## Acceptance criteria

- [ ] Replaying the same Idempotency-Key never places a second order (test with the fake connector).
- [ ] If Zepto fails mid-checkout, the response contains the Zepto leg as a tier C hand-off and no duplicate order.
- [ ] No payment instrument data is accepted or stored by any endpoint.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-033: Checkout router: re-check, tier A orders, tier C hand-off steps` with acceptance criteria ticked.
