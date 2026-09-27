---
id: MND-007
title: "Security baseline, token encryption library and DPDP notices"
epic: PLAT
prd: F1,F8
status: todo
owner: agent
size: M
depends_on: [MND-003]
---

# MND-007 — Security baseline, token encryption library and DPDP notices

**Why:** Store OAuth tokens are the most sensitive data Mandi holds; encryption must exist before any connector stores a token.

Epic `PLAT` · PRD F1,F8 · Size M (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-003

## Read first

- [docs/lld/security-privacy.md](../../docs/lld/security-privacy.md)
- [docs/lld/store-connectors.md#security](../../docs/lld/store-connectors.md#security)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] packages/crypto: envelope encryption helpers (KMS GenerateDataKey, AES-256-GCM, key id and version in ciphertext header), with a local-dev fake KMS.
- [ ] pino redaction config shared by api and workers (tokens, OTPs, phone numbers).
- [ ] Consent notice texts (versioned markdown) for order-history import, email detection, analytics and marketing, plus the privacy policy outline for legal review.
- [ ] Threat-model checklist in docs/lld/security-privacy.md turned into CI-checkable items where possible.

## Acceptance criteria

- [ ] Round-trip encrypt/decrypt tests pass; tampering with ciphertext fails authentication.
- [ ] Log output in tests never contains a token or OTP (asserted).
- [ ] Consent texts carry a version id referenced by the consents table.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-007: Security baseline, token encryption library and DPDP notices` with acceptance criteria ticked.
