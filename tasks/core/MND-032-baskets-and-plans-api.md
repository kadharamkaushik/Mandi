---
id: MND-032
title: "Baskets and plans API"
epic: CORE
prd: F4
status: todo
owner: agent
size: M
depends_on: [MND-031, MND-030, MND-023, MND-025]
---

# MND-032 — Baskets and plans API

**Why:** Turns the current basket plus live offers and fee rules into the three plans the app shows.

Epic `CORE` · PRD F4 · Size M (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-031
- MND-030
- MND-023
- MND-025

## Read first

- [docs/lld/api.md#key-payloads](../../docs/lld/api.md#key-payloads)
- [docs/hld.md#42-plan-and-check-out-a-basket](../../docs/hld.md#42-plan-and-check-out-a-basket)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] baskets module: GET /baskets/current, item add/edit/remove, POST /baskets/current/plans.
- [ ] Offer loading: Valkey hot cache, stale-while-revalidate via offers.refresh, live tier A search through the user's link for linked stores.
- [ ] Persist plans, legs and lines with input_hash and fee rule ids; plans expire after 10 minutes.
- [ ] Expose plan health summary via @mandi/health.

## Acceptance criteria

- [ ] p95 under 800 ms for a 30-item basket with warm cache (load test).
- [ ] Recomputing with the same inputs returns the same input_hash and totals.
- [ ] An expired plan cannot be checked out (409 plan_stale).

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-032: Baskets and plans API` with acceptance criteria ticked.
