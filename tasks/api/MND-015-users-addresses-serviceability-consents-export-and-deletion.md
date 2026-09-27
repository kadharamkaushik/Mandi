---
id: MND-015
title: "Users, addresses, serviceability, consents, export and deletion"
epic: API
prd: F1,F8
status: todo
owner: agent
size: M
depends_on: [MND-014]
---

# MND-015 — Users, addresses, serviceability, consents, export and deletion

**Why:** Profile basics and DPDP rights are needed before any personal data flows in.

Epic `API` · PRD F1,F8 · Size M (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-014

## Read first

- [docs/lld/api.md#endpoints](../../docs/lld/api.md#endpoints)
- [docs/lld/data-model.md#places-and-stores](../../docs/lld/data-model.md#places-and-stores)
- [docs/lld/security-privacy.md#dpdp-act-2023-and-rules-2025](../../docs/lld/security-privacy.md#dpdp-act-2023-and-rules-2025)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] users module: GET/PATCH /me, GET/PUT /me/consents, POST /me/export (async job writes JSON to the exports bucket, 7-day signed URL), DELETE /me (30-day hard delete job).
- [ ] places module: address CRUD with PostGIS point, GET /addresses/{id}/serviceability from store_serviceability.
- [ ] Audit log entries for consent changes, export and deletion.

## Acceptance criteria

- [ ] Deleting an account removes the rows listed in data-model.md#deletion after the job runs (integration test with time travel).
- [ ] Serviceability for a Hyderabad pincode returns only stores seeded as serviceable there.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-015: Users, addresses, serviceability, consents, export and deletion` with acceptance criteria ticked.
