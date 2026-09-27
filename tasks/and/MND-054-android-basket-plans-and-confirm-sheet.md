---
id: MND-054
title: "Android basket plans and confirm sheet"
epic: AND
prd: F4
status: todo
owner: agent
size: M
depends_on: [MND-052, MND-032]
---

# MND-054 — Android basket plans and confirm sheet

**Why:** The plan screen compares cheapest, fewest taps and single store with every fee visible.

Epic `AND` · PRD F4 · Size M (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-052
- MND-032

## Read first

- [docs/lld/android.md](../../docs/lld/android.md)
- [docs/lld/optimiser.md](../../docs/lld/optimiser.md)
- [docs/lld/api.md#key-payloads](../../docs/lld/api.md#key-payloads)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] Plan choice screen with the three plans, fee lines per store and tier labels.
- [ ] Confirm sheet listing each store's items, subtotal, fees, ETA and tier; address and payment-method display (no payment input).
- [ ] Handle plan_stale by recomputing silently; show price_changed diffs for review.

## Acceptance criteria

- [ ] The PRD sample basket shows ₹393 / ₹412 / ₹429 against the seeded API.
- [ ] Every total shown equals the API value (no client-side arithmetic).

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-054: Android basket plans and confirm sheet` with acceptance criteria ticked.
