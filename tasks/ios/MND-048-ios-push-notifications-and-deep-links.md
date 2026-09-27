---
id: MND-048
title: "iOS push notifications and deep links"
epic: IOS
prd: F9
status: todo
owner: agent
size: M
depends_on: [MND-040, MND-037]
---

# MND-048 — iOS push notifications and deep links

**Why:** The basket-due push should land the user one tap from confirming.

Epic `IOS` · PRD F9 · Size M (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-040
- MND-037

## Read first

- [docs/lld/ios.md](../../docs/lld/ios.md)
- [docs/lld/backend.md#workers](../../docs/lld/backend.md#workers)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] APNs with actionable 'Review basket' notification and Live Activity push token; device registration with the API.
- [ ] universal links (apple-app-site-association) for mandi.app paths routed to Home, confirm sheet, order detail.
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
- [ ] Pull request titled `MND-048: iOS push notifications and deep links` with acceptance criteria ticked.
