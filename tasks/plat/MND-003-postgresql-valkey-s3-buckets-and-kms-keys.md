---
id: MND-003
title: "PostgreSQL, Valkey, S3 buckets and KMS keys"
epic: PLAT
prd: F10
status: todo
owner: agent
size: M
depends_on: [MND-002]
---

# MND-003 — PostgreSQL, Valkey, S3 buckets and KMS keys

**Why:** The API and workers need a database with PostGIS/pg_trgm/pgvector/pg_partman, a Valkey instance for cache and queues, S3 buckets and a KMS key for store-token encryption.

Epic `PLAT` · PRD F10 · Size M (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-002

## Read first

- [docs/lld/infra.md#data-stores](../../docs/lld/infra.md#data-stores)
- [docs/lld/data-model.md](../../docs/lld/data-model.md)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] OpenTofu modules rds-postgres (PostgreSQL 16, parameter group enabling the extensions), valkey (ElastiCache for Valkey 8, TLS+AUTH), s3 (feeds-raw, exports, assets with lifecycle rules), kms (store-token CMK).
- [ ] Secrets in AWS Secrets Manager; ExternalSecret manifests for api and workers.
- [ ] IAM roles for service accounts (IRSA or Pod Identity) granting api/workers KMS Encrypt/Decrypt on the store-token key only.

## Acceptance criteria

- [ ] From a debug pod: `CREATE EXTENSION postgis, pg_trgm, vector, pg_partman` succeeds.
- [ ] Valkey accepts TLS connections only.
- [ ] api service account can call kms:GenerateDataKey; a different service account cannot.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-003: PostgreSQL, Valkey, S3 buckets and KMS keys` with acceptance criteria ticked.
