---
id: MND-042
title: "iOS Home and My List"
epic: IOS
prd: F2,F4
status: todo
owner: agent
size: L
depends_on: [MND-040, MND-030, MND-032]
---

# MND-042 — iOS Home and My List

**Why:** Home shows the navy summary card with the basket total and saving, and the usuals list; My List manages cadence and rules.

Epic `IOS` · PRD F2,F4 · Size L (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-040
- MND-030
- MND-032

## Read first

- [docs/lld/ios.md](../../docs/lld/ios.md)
- [docs/lld/api.md#endpoints](../../docs/lld/api.md#endpoints)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] Home: navy hero card (total, coral 'Save ₹…' chip, stores and ETA), usuals with round checkboxes, grade pills, coral CTA.
- [ ] Toggling an item updates the basket and recomputes plans.
- [ ] My List: tabs (all, due soon, weekly, monthly), auto-reorder switch, healthier swap card, edit usual (quantity, cadence, store rule, brand rule), pause flow.
- [ ] Offline: last basket and list shown from local cache.

## Acceptance criteria

- [ ] Unticking an item updates the hero total within 1 s on a mid-range device.
- [ ] Edits round-trip to the API and survive app restart.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-042: iOS Home and My List` with acceptance criteria ticked.
