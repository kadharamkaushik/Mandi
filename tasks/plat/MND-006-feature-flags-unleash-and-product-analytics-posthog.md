---
id: MND-006
title: "Feature flags (Unleash) and product analytics (PostHog)"
epic: PLAT
prd: F10
status: todo
owner: agent
size: S
depends_on: [MND-002, MND-003]
---

# MND-006 — Feature flags (Unleash) and product analytics (PostHog)

**Why:** Tier A for Instamart, tier B, Insights and swaps ship behind flags; PRD metrics need an event pipeline.

Epic `PLAT` · PRD F10 · Size S (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-002
- MND-003

## Read first

- [docs/hld.md#2-components](../../docs/hld.md#2-components)
- [docs/lld/backend.md#cross-cutting](../../docs/lld/backend.md#cross-cutting)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] Deploy Unleash (self-hosted) with PostgreSQL schema; create flags instamart_tier_a, tier_b_cart_fill, insights, swaps.
- [ ] PostHog project; define the event taxonomy in docs/analytics-events.md (activation, plan_computed, checkout_started, handoff_confirmed, order_placed) with no PII in properties.
- [ ] Server and mobile SDK keys stored in Secrets Manager / app config.

## Acceptance criteria

- [ ] Flags can be toggled per user id in dev and are read by a sample endpoint.
- [ ] docs/analytics-events.md lists every event with properties and the PRD metric it feeds.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-006: Feature flags (Unleash) and product analytics (PostHog)` with acceptance criteria ticked.
