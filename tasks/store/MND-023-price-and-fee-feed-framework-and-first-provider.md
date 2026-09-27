---
id: MND-023
title: "Price and fee feed framework and first provider"
epic: STORE
prd: F3,F4
status: todo
owner: agent
size: L
depends_on: [MND-020, MND-011, MND-064]
---

# MND-023 — Price and fee feed framework and first provider

**Why:** Blinkit, BB Now and FirstClub have no ordering API; their prices and fees must come from a contracted, legally cleared source.

Epic `STORE` · PRD F3,F4 · Size L (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-020
- MND-011
- MND-064

## Read first

- [docs/lld/store-connectors.md#feeds-prices-for-tier-c-stores](../../docs/lld/store-connectors.md#feeds-prices-for-tier-c-stores)
- [docs/lld/backend.md#workers](../../docs/lld/backend.md#workers)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] FeedProvider interface; normaliser to Offer and FeeRule rows tagged with source.
- [ ] First provider implementation for the source chosen in MND-064.
- [ ] Workers: offers.refresh every 15 min per pincode cluster and on demand for stale items; fees.refresh daily with change review queue.
- [ ] Valkey hot cache of latest offer per store product and pincode cluster.

## Acceptance criteria

- [ ] Offers for the top 500 seeded products refresh within 15 minutes in staging.
- [ ] A fee rule change creates a review item instead of silently changing plans.
- [ ] Every offer row records its source.

## Notes

No scraping of logged-in sessions or unofficial wrappers (ADR-0007).

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-023: Price and fee feed framework and first provider` with acceptance criteria ticked.
