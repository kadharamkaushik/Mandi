---
id: MND-050
title: "Android app foundation, design system and API client"
epic: AND
prd: F10
status: todo
owner: agent
size: M
depends_on: [MND-013]
---

# MND-050 — Android app foundation, design system and API client

**Why:** Every Android feature task builds on this shell: navigation, theme from the Navy & Coral tokens, and the generated API client.

Epic `AND` · PRD F10 · Size M (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-013

## Read first

- [docs/lld/android.md](../../docs/lld/android.md)
- [packages/design-tokens/tokens.json](../../packages/design-tokens/tokens.json)
- [packages/contracts/openapi.yaml](../../packages/contracts/openapi.yaml)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] Gradle KTS project with version catalog and build-logic convention plugins; modules per docs/lld/android.md.
- [ ] Style Dictionary build generating Tokens.kt from packages/design-tokens; Sora font; components PillButton, NavyHeroCard, GradePill, StoreBadge, PillNavBar.
- [ ] core/network generated with openapi-generator (retrofit2 + kotlinx.serialization), auth interceptor + Authenticator, Idempotency-Key and traceparent.
- [ ] Hilt, Room, DataStore wiring; GitHub Actions workflow for tests and bundle.

## Acceptance criteria

- [ ] The app launches to a placeholder Home using the design system on a Android device.
- [ ] Changing a colour in tokens.json and rebuilding updates the app theme.
- [ ] A sample authenticated call succeeds against the local API.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-050: Android app foundation, design system and API client` with acceptance criteria ticked.
