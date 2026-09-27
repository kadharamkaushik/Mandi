---
id: MND-024
title: "Deep links and hand-off verification for tier C stores"
epic: STORE
prd: F5
status: todo
owner: agent
size: M
depends_on: [MND-020]
---

# MND-024 — Deep links and hand-off verification for tier C stores

**Why:** Tier C hand-off quality depends on links that open the right product in each store app.

Epic `STORE` · PRD F5 · Size M (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-020

## Read first

- [docs/lld/store-connectors.md#deep-links-tier-c](../../docs/lld/store-connectors.md#deep-links-tier-c)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] deepLink() for Blinkit, BB Now and FirstClub returning appUrl, webUrl and searchFallback.
- [ ] Research and record which URL patterns open product pages in each store's iOS and Android apps.
- [ ] Nightly verification job (Android emulator + iOS simulator via Maestro) opening a sample of links; patterns failing twice switch to search fallback automatically.

## Acceptance criteria

- [ ] Link pattern table committed in docs/lld/store-connectors.md with the date verified.
- [ ] A broken pattern flips to search fallback and raises an alert.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-024: Deep links and hand-off verification for tier C stores` with acceptance criteria ticked.
