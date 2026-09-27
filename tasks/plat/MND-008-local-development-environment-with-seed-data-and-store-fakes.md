---
id: MND-008
title: "Local development environment with seed data and store fakes"
epic: PLAT
prd: F10
status: todo
owner: agent
size: S
depends_on: [MND-010, MND-012, MND-020]
---

# MND-008 — Local development environment with seed data and store fakes

**Why:** Agents and developers need a one-command local stack to build and test features without real store accounts.

Epic `PLAT` · PRD F10 · Size S (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-010
- MND-012
- MND-020

## Read first

- [docs/lld/infra.md#local-development](../../docs/lld/infra.md#local-development)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] docker-compose.yml: PostgreSQL 16 + PostGIS, Valkey 8, MinIO, Unleash.
- [ ] Seed script: Bengaluru and Hyderabad pincodes, five stores with capabilities and fee rules, 200 products with offers and nutrition facts, a demo user with usuals.
- [ ] `pnpm dev` runs api and workers against FakeStoreConnector.

## Acceptance criteria

- [ ] From a clean clone, `docker compose up -d && pnpm i && pnpm db:migrate && pnpm db:seed && pnpm dev` serves /v1/health in under 5 minutes.
- [ ] Seeded demo basket reproduces the PRD example: ₹393 split, ₹412 single store, ₹429 three stores.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-008: Local development environment with seed data and store fakes` with acceptance criteria ticked.
