---
id: MND-061
title: "Plan accuracy harness"
epic: QA
prd: F4
status: todo
owner: agent
size: M
depends_on: [MND-032]
---

# MND-061 — Plan accuracy harness

**Why:** The PRD promises totals within ₹2 of store checkout on 95% of baskets.

Epic `QA` · PRD F4 · Size M (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-032

## Read first

- [docs/prd.md#mvp-success-metrics](../../docs/prd.md#mvp-success-metrics)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] Script that builds sample baskets in tier A stores (cart only, no order) and compares the store's cart total with Mandi's plan leg.
- [ ] Manual protocol for tier C stores: weekly sample of 20 baskets checked by a human, results logged.
- [ ] Grafana panel for accuracy by store.

## Acceptance criteria

- [ ] Accuracy report for 100 baskets per store before pilot gate.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-061: Plan accuracy harness` with acceptance criteria ticked.
