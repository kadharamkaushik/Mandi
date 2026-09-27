---
id: MND-030
title: "Usuals: import, cadence inference, CRUD, pause and due scheduler"
epic: CORE
prd: F1,F2,F9
status: todo
owner: agent
size: L
depends_on: [MND-015, MND-021, MND-011]
---

# MND-030 — Usuals: import, cadence inference, CRUD, pause and due scheduler

**Why:** The usuals list is Mandi's moat: what this household reorders and when.

Epic `CORE` · PRD F1,F2,F9 · Size L (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-015
- MND-021
- MND-011

## Read first

- [docs/lld/data-model.md#usuals-baskets-and-orders](../../docs/lld/data-model.md#usuals-baskets-and-orders)
- [docs/lld/api.md#endpoints](../../docs/lld/api.md#endpoints)
- [docs/lld/backend.md#workers](../../docs/lld/backend.md#workers)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] usuals.import job: read Zepto order history, map items to canonical products, create usuals for items bought 2+ times.
- [ ] Cadence inference: median gap between purchases, clamped 1–30 days, recalculated on each confirmed order.
- [ ] Endpoints: GET/POST/PATCH/DELETE /usuals, POST /usuals/import, POST /usuals/pause.
- [ ] usuals.due hourly job: add due items to the current basket and enqueue basket-due notifications.

## Acceptance criteria

- [ ] Given a fixture order history, the imported list and cadences match expected values.
- [ ] Pausing Thu–Sun moves due dates past the pause and restores cadence after.
- [ ] Editing cadence recalculates next_due_on immediately.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-030: Usuals: import, cadence inference, CRUD, pause and due scheduler` with acceptance criteria ticked.
