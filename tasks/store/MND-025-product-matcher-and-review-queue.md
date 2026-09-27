---
id: MND-025
title: "Product matcher and review queue"
epic: STORE
prd: F3,F4
status: todo
owner: agent
size: L
depends_on: [MND-012, MND-023]
---

# MND-025 — Product matcher and review queue

**Why:** The same product must be recognised across stores, and different pack sizes must never be merged.

Epic `STORE` · PRD F3,F4 · Size L (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-012
- MND-023

## Read first

- [docs/lld/data-model.md#catalogue-and-prices](../../docs/lld/data-model.md#catalogue-and-prices)
- [docs/lld/backend.md#workers](../../docs/lld/backend.md#workers)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] Normaliser: brand, variant and pack size/unit parsing from titles (g, kg, ml, l, pc, packs of N).
- [ ] Candidate generation with pg_trgm and pgvector embeddings (local open-source sentence-embedding model); scoring with pack size as a hard constraint.
- [ ] Auto-confirm ≥ 0.92, review 0.75–0.92; CLI/admin endpoint for reviewers.
- [ ] Seed: manually confirmed matches for the top 2,000 staples in BLR and HYD.

## Acceptance criteria

- [ ] On a labelled set of 500 pairs: precision ≥ 99% for auto-confirmed matches, recall ≥ 90%.
- [ ] Different pack sizes are never auto-matched (property test).

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-025: Product matcher and review queue` with acceptance criteria ticked.
