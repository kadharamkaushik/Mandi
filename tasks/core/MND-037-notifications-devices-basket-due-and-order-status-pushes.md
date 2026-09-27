---
id: MND-037
title: "Notifications: devices, basket-due and order-status pushes"
epic: CORE
prd: F9
status: todo
owner: agent
size: M
depends_on: [MND-030, MND-036]
---

# MND-037 — Notifications: devices, basket-due and order-status pushes

**Why:** The 'basket is ready' push is the fastest path into a two-tap reorder.

Epic `CORE` · PRD F9 · Size M (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-030
- MND-036

## Read first

- [docs/lld/backend.md#workers](../../docs/lld/backend.md#workers)
- [docs/lld/ios.md#platform-features](../../docs/lld/ios.md#platform-features)
- [docs/lld/android.md#platform-features](../../docs/lld/android.md#platform-features)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] POST/DELETE /devices; APNs (token auth) and FCM HTTP v1 senders in workers.
- [ ] basket_due notification at the user's preferred hour with deep link to the confirm sheet; order status pushes; iOS Live Activity push updates for hand-off progress.
- [ ] Quiet hours 22:00–07:00 IST; per-user daily cap of 3.

## Acceptance criteria

- [ ] End-to-end in staging: due usual → push received on a test iPhone and Android device → opens confirm sheet.
- [ ] Invalid tokens are pruned after provider errors.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-037: Notifications: devices, basket-due and order-status pushes` with acceptance criteria ticked.
