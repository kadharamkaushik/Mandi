---
id: MND-010
title: "Bootstrap the NestJS API service"
epic: API
prd: F10
status: todo
owner: agent
size: M
depends_on: []
---

# MND-010 — Bootstrap the NestJS API service

**Why:** The API is a NestJS modular monolith. This task creates the skeleton every feature module plugs into.

Epic `API` · PRD F10 · Size M (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- Nothing; can start now.

## Read first

- [docs/lld/backend.md](../../docs/lld/backend.md)
- [docs/adr/0002-nestjs-modular-monolith-for-the-backend.md](../../docs/adr/0002-nestjs-modular-monolith-for-the-backend.md)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] services/api: NestJS 11 with Fastify adapter, strict TypeScript, Zod-validated config, pino logger with redaction, OpenTelemetry auto-instrumentation.
- [ ] common/: problem-details exception filter (RFC 9457), auth guard stub with @Public(), idempotency interceptor, cursor pagination helpers, rate-limit guard on Valkey.
- [ ] Empty module folders from backend.md with eslint-plugin-boundaries rules enforcing facade-only imports.
- [ ] GET /v1/health (liveness) and /v1/ready (DB + Valkey).
- [ ] Dockerfile (distroless, non-root) and Helm chart in infra/k8s/charts/api.

## Acceptance criteria

- [ ] `pnpm --filter api test` runs a smoke test with Testcontainers.
- [ ] Importing another module's internal file fails lint.
- [ ] Errors return application/problem+json with a stable `code`.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-010: Bootstrap the NestJS API service` with acceptance criteria ticked.
