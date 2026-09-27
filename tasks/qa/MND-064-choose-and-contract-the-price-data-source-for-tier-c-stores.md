---
id: MND-064
title: "Choose and contract the price data source for tier C stores"
epic: QA
prd: F3,F4
status: todo
owner: human
size: M
depends_on: []
---

# MND-064 — Choose and contract the price data source for tier C stores

**Why:** MND-023 cannot start its first provider until a legally cleared price source is chosen.

Epic `QA` · PRD F3,F4 · Size M (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: human

## Depends on

- Nothing; can start now.

## Read first

- [docs/lld/store-connectors.md#feeds-prices-for-tier-c-stores](../../docs/lld/store-connectors.md#feeds-prices-for-tier-c-stores)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] Evaluate licensed data vendors, affiliate feeds and direct partnerships for Blinkit, BB Now and FirstClub in BLR and HYD.
- [ ] Criteria: coverage of top 2,000 staples, refresh frequency ≤ 15 min, fee data, legal terms, cost.
- [ ] Sign the chosen source and share API credentials via Secrets Manager.

## Acceptance criteria

- [ ] Decision recorded as ADR-0009 with alternatives and cost.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-064: Choose and contract the price data source for tier C stores` with acceptance criteria ticked.
