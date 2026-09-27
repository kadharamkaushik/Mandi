---
id: MND-021
title: "Zepto MCP connector with OAuth link flow"
epic: STORE
prd: F1,F5,F6
status: todo
owner: agent
size: L
depends_on: [MND-020, MND-007, MND-026]
---

# MND-021 — Zepto MCP connector with OAuth link flow

**Why:** Zepto's official MCP server lets Mandi search, build carts, place orders and read order history for a logged-in user. This is Mandi's first tier A store.

Epic `STORE` · PRD F1,F5,F6 · Size L (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-020
- MND-007
- MND-026

## Read first

- [docs/lld/store-connectors.md#zepto-tier-a](../../docs/lld/store-connectors.md#zepto-tier-a)
- [docs/hld.md#41-link-zepto-oauth--otp](../../docs/hld.md#41-link-zepto-oauth--otp)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] POST /store-links/zepto/start (PKCE + state) and GET /oauth/zepto/callback exchanging the code, encrypting tokens with packages/crypto, storing store_links.
- [ ] Zepto connector using @modelcontextprotocol/sdk (streamable HTTP): discover tools at startup, map to search/offers/buildCart/placeOrder/orderStatus/orderHistory in zepto.tools.ts.
- [ ] Token refresh and link expiry handling (status expired → user prompted to relink).
- [ ] Contract tests against recorded MCP responses; a manual smoke script for a real test account.

## Acceptance criteria

- [ ] With a test account in staging: link, search 'amul taaza', build a 2-item cart and fetch order history.
- [ ] placeOrder is only callable from the checkout module with an idempotency key (enforced by type).
- [ ] No token appears in logs or traces (asserted in tests).

## Notes

Blocked in production until Zepto allowlists the production redirect URI (MND-026).

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-021: Zepto MCP connector with OAuth link flow` with acceptance criteria ticked.
