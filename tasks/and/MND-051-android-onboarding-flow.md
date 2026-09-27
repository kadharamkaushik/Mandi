---
id: MND-051
title: "Android onboarding flow"
epic: AND
prd: F1
status: todo
owner: agent
size: L
depends_on: [MND-050, MND-014, MND-015, MND-021, MND-030, MND-034]
---

# MND-051 — Android onboarding flow

**Why:** Six screens from the design canvas: welcome, phone + OTP, delivery location, link stores, confirm usuals, health goals.

Epic `AND` · PRD F1 · Size L (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-050
- MND-014
- MND-015
- MND-021
- MND-030
- MND-034

## Read first

- [docs/lld/android.md](../../docs/lld/android.md)
- [docs/prd.md](../../docs/prd.md)
- [docs/lld/api.md#endpoints](../../docs/lld/api.md#endpoints)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] Phone entry and OTP with SMS User Consent API; tokens stored in Android Keystore-backed encrypted storage.
- [ ] Location by GPS or search; serviceability list with ETAs.
- [ ] Link Zepto via Custom Tabs; other stores shown as 'compared, not linked'.
- [ ] Usuals import progress and the untick list; health goals, diet and avoid chips.
- [ ] Consent notices shown before order-history import (consent recorded).

## Acceptance criteria

- [ ] A new user reaches Home with at least 5 usuals in under 3 minutes (timed test on a real device).
- [ ] Declining the Zepto link still reaches Home with a manual quick-pick list.
- [ ] All controls have accessibility labels and 44 pt / 48 dp targets.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-051: Android onboarding flow` with acceptance criteria ticked.
