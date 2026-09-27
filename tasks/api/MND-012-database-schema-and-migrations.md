---
id: MND-012
title: "Database schema and migrations"
epic: API
prd: F1–F9
status: todo
owner: agent
size: M
depends_on: [MND-010]
---

# MND-012 — Database schema and migrations

**Why:** Every feature depends on the schema in data-model.md.

Epic `API` · PRD F1–F9 · Size M (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-010

## Read first

- [docs/lld/data-model.md](../../docs/lld/data-model.md)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] packages/db with Drizzle schema for all tables in data-model.md, enums as PostgreSQL enums, UUIDv7 ids, money in paise.
- [ ] Migrations enabling extensions; pg_partman daily partitions for offers with 90-day retention.
- [ ] Indexes listed in data-model.md.
- [ ] Repository helpers for transactions and the outbox write.

## Acceptance criteria

- [ ] `pnpm db:migrate` applies cleanly to an empty database and is idempotent.
- [ ] Schema tests assert every table and index in data-model.md exists.
- [ ] Offers older than 90 days are dropped by the partman maintenance job in a test.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-012: Database schema and migrations` with acceptance criteria ticked.
