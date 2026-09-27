---
id: MND-055
title: "Android checkout: tier A orders and tier C hand-off"
epic: AND
prd: F5
status: todo
owner: agent
size: L
depends_on: [MND-054, MND-033, MND-024]
---

# MND-055 — Android checkout: tier A orders and tier C hand-off

**Why:** The two-tap moment: confirm places tier A orders, then guides the user through each tier C store.

Epic `AND` · PRD F5 · Size L (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-054
- MND-033
- MND-024

## Read first

- [docs/lld/android.md](../../docs/lld/android.md)
- [docs/hld.md#3-checkout-tiers](../../docs/hld.md#3-checkout-tiers)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] Confirm → POST checkout with an Idempotency-Key kept across retries; placing-orders screen with per-store progress.
- [ ] Tier C: open each store via verified App Links (assetlinks.json) or web fallback; hand-off checklist as a conversation notification bubble (Android 11+) with sticky-notification fallback on 8–10, ticking items as the user returns or taps.
- [ ] 'Copy list' fallback and per-store 'Did it go through?' prompt on return.
- [ ] Partial failure UI: a failed tier A store becomes a hand-off step.

## Acceptance criteria

- [ ] A two-store basket (Zepto tier A + Blinkit tier C) completes in ≤ 4 taps plus in-app adds (measured in the usability script).
- [ ] Killing the app during checkout and relaunching never places a duplicate order.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-055: Android checkout: tier A orders and tier C hand-off` with acceptance criteria ticked.
