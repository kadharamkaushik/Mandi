---
id: MND-063
title: "Legal and compliance review before pilot"
epic: QA
prd: F8,F10
status: todo
owner: human
size: M
depends_on: [MND-007]
---

# MND-063 — Legal and compliance review before pilot

**Why:** Store terms, the price-data route, DPDP notices and health disclaimers need Indian counsel before real users.

Epic `QA` · PRD F8,F10 · Size M (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: human

## Depends on

- MND-007

## Read first

- [docs/lld/security-privacy.md](../../docs/lld/security-privacy.md)
- [docs/prd.md](../../docs/prd.md)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] Review Zepto and Swiggy MCP terms for third-party commercial use.
- [ ] Approve privacy policy, consent notices and grievance officer details.
- [ ] Approve health-grade wording ('guidance, not medical advice').

## Acceptance criteria

- [ ] Signed-off documents linked from docs/lld/security-privacy.md.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-063: Legal and compliance review before pilot` with acceptance criteria ticked.
