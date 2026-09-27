---
id: MND-013
title: "Complete the OpenAPI contract and code generation"
epic: API
prd: F1–F9
status: todo
owner: agent
size: M
depends_on: [MND-010]
---

# MND-013 — Complete the OpenAPI contract and code generation

**Why:** iOS, Android and the API are built in parallel from one contract; the starter spec covers only auth and checkout.

Epic `API` · PRD F1–F9 · Size M (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-010

## Read first

- [docs/lld/api.md](../../docs/lld/api.md)
- [packages/contracts/openapi.yaml](../../packages/contracts/openapi.yaml)
- [docs/adr/0005-contract-first-api-with-openapi-31.md](../../docs/adr/0005-contract-first-api-with-openapi-31.md)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] Add every endpoint in api.md with request/response schemas, problem codes and examples.
- [ ] Spectral rules: operationId, tags, examples on 2xx responses, no inline schemas for shared types.
- [ ] Server: generated TypeScript types + runtime validation wired into controllers.
- [ ] Publish generated clients as build steps for iOS (swift-openapi-generator config) and Android (openapi-generator Gradle task).

## Acceptance criteria

- [ ] `pnpm contracts:lint` passes with zero warnings.
- [ ] A response that violates the spec fails the API contract test suite.
- [ ] iOS and Android sample calls compile against the generated clients.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-013: Complete the OpenAPI contract and code generation` with acceptance criteria ticked.
