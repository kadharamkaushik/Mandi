---
id: MND-043
title: "iOS search and product page"
epic: IOS
prd: F3,F7
status: todo
owner: agent
size: M
depends_on: [MND-040, MND-035]
---

# MND-043 — iOS search and product page

**Why:** Search once, see every store's price; product page shows health grade and store offers.

Epic `IOS` · PRD F3,F7 · Size M (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-040
- MND-035

## Read first

- [docs/lld/ios.md](../../docs/lld/ios.md)
- [docs/lld/api.md#endpoints](../../docs/lld/api.md#endpoints)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] Search home: recents, buy-again row, categories.
- [ ] Results: merged product cards with per-store price strip and best-price highlight; filters.
- [ ] Product page: grade and nutrition bars, store price list with ETA, quantity stepper, 'Add' → make-it-a-usual sheet.

## Acceptance criteria

- [ ] Search results render in under 300 ms after the API responds.
- [ ] Adding as a usual with a cadence creates it via the API.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-043: iOS search and product page` with acceptance criteria ticked.
