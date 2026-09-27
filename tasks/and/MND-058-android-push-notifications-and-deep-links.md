---
id: MND-058
title: "Android push notifications and deep links"
epic: AND
prd: F9
status: todo
owner: agent
size: M
depends_on: [MND-050, MND-037]
---

# MND-058 — Android push notifications and deep links

**Why:** The basket-due push should land the user one tap from confirming.

Epic `AND` · PRD F9 · Size M (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-050
- MND-037

## Read first

- [docs/lld/android.md](../../docs/lld/android.md)
- [docs/lld/backend.md#workers](../../docs/lld/backend.md#workers)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] FCM data messages rendered as local notifications with a 'Review basket' action; device registration with the API.
- [ ] verified App Links (assetlinks.json) for mandi.app paths routed to Home, confirm sheet, order detail.
- [ ] Notification permission prompt after the first successful plan, not at launch.

## Acceptance criteria

- [ ] Tapping a basket-due push opens the confirm sheet with a fresh plan.
- [ ] Links open the right screen from cold start and from background.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-058: Android push notifications and deep links` with acceptance criteria ticked.
