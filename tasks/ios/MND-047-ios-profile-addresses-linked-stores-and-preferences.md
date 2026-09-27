---
id: MND-047
title: "iOS profile, addresses, linked stores and preferences"
epic: IOS
prd: F8
status: todo
owner: agent
size: M
depends_on: [MND-040, MND-015, MND-034]
---

# MND-047 — iOS profile, addresses, linked stores and preferences

**Why:** Account management and DPDP rights inside the app.

Epic `IOS` · PRD F8 · Size M (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-040
- MND-015
- MND-034

## Read first

- [docs/lld/ios.md](../../docs/lld/ios.md)
- [docs/lld/security-privacy.md#dpdp-act-2023-and-rules-2025](../../docs/lld/security-privacy.md#dpdp-act-2023-and-rules-2025)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] Profile summary, addresses with store coverage, payment method display per tier A store, linked stores (link/unlink, last sync), health & diet, notifications settings.
- [ ] Consents screen; data export request; delete account with confirmation and 30-day notice.
- [ ] Grievance contact and privacy policy links.

## Acceptance criteria

- [ ] Delete account signs the user out and the API schedules deletion.
- [ ] Unlinking Zepto switches Zepto to tier C in the next plan.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-047: iOS profile, addresses, linked stores and preferences` with acceptance criteria ticked.
