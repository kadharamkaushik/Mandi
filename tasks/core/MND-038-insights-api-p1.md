---
id: MND-038
title: "Insights API (P1)"
epic: CORE
prd: F7
status: todo
owner: agent
size: S
depends_on: [MND-036, MND-034]
---

# MND-038 — Insights API (P1)

**Why:** Monthly spend, savings and basket health trends for the Insights screen.

Epic `CORE` · PRD F7 · Size S (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-036
- MND-034

## Read first

- [docs/lld/api.md#endpoints](../../docs/lld/api.md#endpoints)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] GET /insights?month= returning spend, savings, weekly savings series, basket grade shares, habit metrics (added sugar, fresh produce share, ultra-processed share), store wins.
- [ ] Materialised monthly aggregates refreshed nightly.

## Acceptance criteria

- [ ] Numbers reconcile with orders for a seeded month.
- [ ] Endpoint hidden behind the insights flag.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-038: Insights API (P1)` with acceptance criteria ticked.
