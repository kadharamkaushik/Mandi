---
id: MND-020
title: "StoreConnector interface, capability registry and fake connector"
epic: STORE
prd: F3,F4,F5
status: todo
owner: agent
size: M
depends_on: [MND-012]
---

# MND-020 — StoreConnector interface, capability registry and fake connector

**Why:** All store access goes through one interface so tiers can change at runtime without app releases.

Epic `STORE` · PRD F3,F4,F5 · Size M (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-012

## Read first

- [docs/lld/store-connectors.md#interface](../../docs/lld/store-connectors.md#interface)
- [docs/adr/0007-tiered-store-connectors.md](../../docs/adr/0007-tiered-store-connectors.md)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] packages/connectors: StoreConnector interface, Capabilities, error taxonomy (auth_expired, out_of_stock, rate_limited, unavailable).
- [ ] Capability registry reading store_capabilities and link status; tier resolution function with unit tests.
- [ ] FakeStoreConnector driven by fixtures with latency/failure injection.
- [ ] opossum circuit breaker wrapper that downgrades a store to tier C when open.

## Acceptance criteria

- [ ] Resolution table tests: store tier A + link active → A; link expired → C; breaker open → C.
- [ ] Fake connector passes the same contract test suite real connectors must pass.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-020: StoreConnector interface, capability registry and fake connector` with acceptance criteria ticked.
