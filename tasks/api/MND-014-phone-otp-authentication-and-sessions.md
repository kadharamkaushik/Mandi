---
id: MND-014
title: "Phone OTP authentication and sessions"
epic: API
prd: F1
status: todo
owner: agent
size: M
depends_on: [MND-012, MND-013, MND-007]
---

# MND-014 — Phone OTP authentication and sessions

**Why:** Phone number + OTP is the only login. Tokens must be short-lived with rotating refresh tokens.

Epic `API` · PRD F1 · Size M (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-012
- MND-013
- MND-007

## Read first

- [docs/lld/api.md#conventions](../../docs/lld/api.md#conventions)
- [docs/lld/security-privacy.md#threat-model-top-risks](../../docs/lld/security-privacy.md#threat-model-top-risks)
- [docs/lld/data-model.md#identity-and-users](../../docs/lld/data-model.md#identity-and-users)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] identity module: POST /auth/otp, /auth/otp/verify, /auth/refresh, /auth/logout.
- [ ] SmsGateway interface with an MSG91 (or equivalent) adapter using a DLT-registered template, plus a console adapter for dev.
- [ ] EdDSA JWT access tokens (15 min) with kid rotation from Secrets Manager; opaque refresh tokens (30 days) rotated with reuse detection.
- [ ] Limits: 5 attempts per challenge, 5 OTPs per phone per hour, per-IP limits.
- [ ] devices registration on verify.

## Acceptance criteria

- [ ] Reusing an old refresh token revokes the whole session family (test).
- [ ] OTP codes are stored hashed and never logged.
- [ ] Rate limits return 429 with Retry-After.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-014: Phone OTP authentication and sessions` with acceptance criteria ticked.
