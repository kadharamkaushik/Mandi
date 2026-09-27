---
id: MND-031
title: "Basket optimiser package"
epic: CORE
prd: F4
status: todo
owner: agent
size: M
depends_on: []
---

# MND-031 — Basket optimiser package

**Why:** The optimiser decides where each item is bought, including every fee and a friction cost for tier C stores. It is pure code and can start on day one.

Epic `CORE` · PRD F4 · Size M (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- Nothing; can start now.

## Read first

- [docs/lld/optimiser.md](../../docs/lld/optimiser.md)
- [docs/adr/0006-basket-optimiser-by-exact-enumeration-over-store-subsets.md](../../docs/adr/0006-basket-optimiser-by-exact-enumeration-over-store-subsets.md)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] packages/optimiser implementing the algorithm in optimiser.md with typed input/output.
- [ ] Property tests (fast-check) and 30 golden baskets including the PRD example.
- [ ] Benchmark script: 30 items × 8 stores under 5 ms p95 on CI hardware.

## Acceptance criteria

- [ ] Golden tests reproduce ₹393 / ₹412 / ₹429 for the PRD basket.
- [ ] Property: cheapest plan total ≤ every other plan total; no out-of-stock lines in any plan.
- [ ] Coverage ≥ 90% lines.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-031: Basket optimiser package` with acceptance criteria ticked.
