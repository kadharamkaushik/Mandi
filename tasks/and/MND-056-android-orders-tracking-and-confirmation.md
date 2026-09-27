---
id: MND-056
title: "Android orders, tracking and confirmation"
epic: AND
prd: F6
status: todo
owner: agent
size: M
depends_on: [MND-055, MND-036]
---

# MND-056 — Android orders, tracking and confirmation

**Why:** Users see what was ordered where, confirm tier C orders and report issues.

Epic `AND` · PRD F6 · Size M (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-055
- MND-036

## Read first

- [docs/lld/android.md](../../docs/lld/android.md)
- [docs/lld/api.md#endpoints](../../docs/lld/api.md#endpoints)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] Paid / live tracking screen with per-store status; order detail with items, fees and substitution card.
- [ ] Tier C confirmation sheet with amount pre-filled; report-issue flow.
- [ ] Order list in Profile.

## Acceptance criteria

- [ ] Confirming a tier C order updates Home's next-due items.
- [ ] Status changes from the API appear without a manual refresh (push or polling while open).

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-056: Android orders, tracking and confirmation` with acceptance criteria ticked.
