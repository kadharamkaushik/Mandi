---
id: MND-004
title: "Observability stack and alerts"
epic: PLAT
prd: F10
status: todo
owner: agent
size: M
depends_on: [MND-002]
---

# MND-004 — Observability stack and alerts

**Why:** Traces, metrics and logs are needed from the first deployed service to debug connector calls and plan accuracy.

Epic `PLAT` · PRD F10 · Size M (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-002

## Read first

- [docs/lld/infra.md#observability](../../docs/lld/infra.md#observability)
- [docs/lld/backend.md#cross-cutting](../../docs/lld/backend.md#cross-cutting)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] Install OpenTelemetry Collector (DaemonSet + gateway), kube-prometheus-stack, Loki, Tempo and Grafana through Argo CD.
- [ ] Dashboards: API RED per route, BullMQ queue depth/failures, connector calls by store and tier, business counters.
- [ ] Alert rules: API 5xx > 2% for 5 min, p95 latency > 1 s, dead-letter queue non-empty, connector error rate > 10%.

## Acceptance criteria

- [ ] A request to the sample service shows a trace in Tempo linked to its logs in Loki.
- [ ] Alerts route to a test Slack channel.
- [ ] Dashboards are provisioned as code in infra/k8s.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-004: Observability stack and alerts` with acceptance criteria ticked.
