---
id: MND-062
title: "Pilot readiness: KPIs, support runbook and pilot cohort tooling"
epic: QA
prd: F10
status: todo
owner: agent
size: M
depends_on: [MND-006, MND-060]
---

# MND-062 — Pilot readiness: KPIs, support runbook and pilot cohort tooling

**Why:** The closed pilot (300 households in Bengaluru and Hyderabad) needs measurement and support from day one.

Epic `QA` · PRD F10 · Size M (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-006
- MND-060

## Read first

- [docs/prd.md#mvp-success-metrics](../../docs/prd.md#mvp-success-metrics)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] PostHog dashboards for every PRD metric (week-4 retention, baskets per user, hand-off completion, saving per basket, taps to carts).
- [ ] Invite-code gating and cohort flags; in-app feedback link.
- [ ] Support runbook: failed order, wrong price, relink store, delete account.

## Acceptance criteria

- [ ] Dashboards show seeded test data end to end.
- [ ] Runbook reviewed by the product owner.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-062: Pilot readiness: KPIs, support runbook and pilot cohort tooling` with acceptance criteria ticked.
