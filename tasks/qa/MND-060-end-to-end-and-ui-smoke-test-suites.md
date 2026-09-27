---
id: MND-060
title: "End-to-end and UI smoke test suites"
epic: QA
prd: F1–F9
status: todo
owner: agent
size: M
depends_on: [MND-033, MND-045, MND-055]
---

# MND-060 — End-to-end and UI smoke test suites

**Why:** One suite proves the core journey works on both apps against the fake stores.

Epic `QA` · PRD F1–F9 · Size M (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-033
- MND-045
- MND-055

## Read first

- [docs/lld/backend.md#testing](../../docs/lld/backend.md#testing)
- [docs/lld/ios.md#quality](../../docs/lld/ios.md#quality)
- [docs/lld/android.md#quality](../../docs/lld/android.md#quality)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] Maestro flows: onboarding, edit a usual, plan, tier A checkout, tier C hand-off with confirm, delete account.
- [ ] Run on iOS simulator and Android emulator in CI nightly against staging with FakeStoreConnector.
- [ ] API contract tests against the OpenAPI spec for every endpoint.

## Acceptance criteria

- [ ] Nightly run green for 5 consecutive days before pilot.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-060: End-to-end and UI smoke test suites` with acceptance criteria ticked.
