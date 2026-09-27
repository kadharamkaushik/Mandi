---
id: MND-035
title: "Search and product page API"
epic: CORE
prd: F3
status: todo
owner: agent
size: M
depends_on: [MND-025, MND-034, MND-023]
---

# MND-035 — Search and product page API

**Why:** Users search once and see every store's price for the same product.

Epic `CORE` · PRD F3 · Size M (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-025
- MND-034
- MND-023

## Read first

- [docs/lld/api.md#endpoints](../../docs/lld/api.md#endpoints)
- [docs/adr/0008-postgresql-search-before-opensearch.md](../../docs/adr/0008-postgresql-search-before-opensearch.md)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] GET /search with tsvector + pg_trgm ranking, filters (best price, fastest, healthiest, veg only), results merged by canonical product with per-store offers.
- [ ] GET /products/{id}: nutrition, grade and drivers, offers per store with ETA and unit price, 30-day low price.
- [ ] Search analytics event with query and result count (no PII).

## Acceptance criteria

- [ ] p95 search latency under 150 ms on the seeded catalogue.
- [ ] Different pack sizes never appear as the same result card.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-035: Search and product page API` with acceptance criteria ticked.
