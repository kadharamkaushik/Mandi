---
id: MND-026
title: "Store access applications: Zepto allowlist and Swiggy Builders Club"
epic: STORE
prd: F5
status: todo
owner: human
size: S
depends_on: []
---

# MND-026 — Store access applications: Zepto allowlist and Swiggy Builders Club

**Why:** Tier A in production depends on two external approvals with no fixed date; start them now.

Epic `STORE` · PRD F5 · Size S (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: human

## Depends on

- Nothing; can start now.

## Read first

- [docs/prd.md](../../docs/prd.md)
- [docs/lld/store-connectors.md](../../docs/lld/store-connectors.md)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] Raise the redirect URI allowlist request on github.com/zeptonow/mcp with the production domain and callback URL once api.mandi.app is live.
- [ ] Apply to Swiggy Builders Club (builders@swiggy.in) for Instamart production access; ask about payment methods beyond COD and third-party app policy.
- [ ] Record answers and dates in docs/lld/store-connectors.md.

## Acceptance criteria

- [ ] Written confirmation (or rejection) from each is linked in the doc.
- [ ] Store capability records are set to match what was approved.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-026: Store access applications: Zepto allowlist and Swiggy Builders Club` with acceptance criteria ticked.
