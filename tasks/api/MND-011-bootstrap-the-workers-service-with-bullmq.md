---
id: MND-011
title: "Bootstrap the workers service with BullMQ"
epic: API
prd: F10
status: todo
owner: agent
size: S
depends_on: [MND-010]
---

# MND-011 — Bootstrap the workers service with BullMQ

**Why:** Background jobs (prices, matching, schedules, polling, notifications) run in a separate deployable sharing the API's packages.

Epic `API` · PRD F10 · Size S (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-010

## Read first

- [docs/lld/backend.md#workers](../../docs/lld/backend.md#workers)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] services/workers: NestJS standalone app, BullMQ queues from backend.md with retry/backoff defaults and dead-letter queues.
- [ ] Repeatable job scheduler registry; outbox relay loop reading the outbox table.
- [ ] Bull Board (read-only) behind admin auth for queue inspection in dev/staging.
- [ ] Helm chart with KEDA ScaledObject on queue depth.

## Acceptance criteria

- [ ] A test job enqueued via the outbox is processed exactly once even when the worker restarts mid-job.
- [ ] Failed jobs land in the dead-letter queue after max attempts and raise a metric.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-011: Bootstrap the workers service with BullMQ` with acceptance criteria ticked.
