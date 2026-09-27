---
id: MND-022
title: "Instamart MCP connector behind a flag"
epic: STORE
prd: F5
status: todo
owner: agent
size: M
depends_on: [MND-020, MND-026]
---

# MND-022 — Instamart MCP connector behind a flag

**Why:** Swiggy's official Instamart MCP can search, build carts and place orders, but third-party production use needs Builders Club approval and the README currently allows COD only.

Epic `STORE` · PRD F5 · Size M (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-020
- MND-026

## Read first

- [docs/lld/store-connectors.md#instamart-tier-a-behind-flag](../../docs/lld/store-connectors.md#instamart-tier-a-behind-flag)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] Instamart connector mirroring the Zepto one against https://mcp.swiggy.com/im.
- [ ] Everything behind flag instamart_tier_a; when off, Instamart resolves to tier C.
- [ ] Handle the documented session-conflict warning: never run MCP calls while the user is in the Instamart app during hand-off.

## Acceptance criteria

- [ ] With the flag off, plans show Instamart as tier C with feed prices.
- [ ] With the flag on in staging and an approved client, a test order can be placed with the allowed payment method.

## Notes

Do not enable in production without written approval from Swiggy (tracked in MND-026).

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-022: Instamart MCP connector behind a flag` with acceptance criteria ticked.
