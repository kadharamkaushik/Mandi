---
id: MND-036
title: "Orders: status polling, tier C confirmation, substitutions"
epic: CORE
prd: F6
status: todo
owner: agent
size: M
depends_on: [MND-033, MND-011]
---

# MND-036 — Orders: status polling, tier C confirmation, substitutions

**Why:** Savings and next-due dates depend on knowing which orders actually happened.

Epic `CORE` · PRD F6 · Size M (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-033
- MND-011

## Read first

- [docs/lld/api.md#endpoints](../../docs/lld/api.md#endpoints)
- [docs/lld/backend.md#workers](../../docs/lld/backend.md#workers)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] orders.poll job for tier A orders until a terminal status; status mapping per connector.
- [ ] GET /orders, GET /orders/{id}, POST /orders/{id}/confirm (tier C, amount paid pre-filled), POST /orders/{id}/report-issue.
- [ ] On confirmation: usual_events bought, cadence update, savings computed against the plan's best single-store total.

## Acceptance criteria

- [ ] A confirmed tier C order updates next_due_on for its usuals.
- [ ] Tier A status transitions are reflected within 2 minutes in staging.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-036: Orders: status polling, tier C confirmation, substitutions` with acceptance criteria ticked.
