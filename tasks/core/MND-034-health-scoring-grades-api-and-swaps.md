---
id: MND-034
title: "Health scoring, grades API and swaps"
epic: CORE
prd: F7
status: todo
owner: agent
size: M
depends_on: [MND-012]
---

# MND-034 — Health scoring, grades API and swaps

**Why:** Every item and basket shows a grade; swaps suggest healthier items at the same or lower price.

Epic `CORE` · PRD F7 · Size M (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-012

## Read first

- [docs/lld/health.md](../../docs/lld/health.md)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] packages/health implementing rules version 2026.1 with category overrides and goal adjustments.
- [ ] Recompute job on nutrition or rules change; grades stored with drivers.
- [ ] GET/PUT /health-profile, GET /products/{id}/swaps.

## Acceptance criteria

- [ ] Unit tests for each driver band and category override.
- [ ] A product without nutrition facts returns grade null with reason 'no_data'.
- [ ] Swaps never cost more than the current item at the plan's store.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-034: Health scoring, grades API and swaps` with acceptance criteria ticked.
