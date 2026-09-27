---
id: MND-040
title: "iOS app foundation, design system and API client"
epic: IOS
prd: F10
status: todo
owner: agent
size: M
depends_on: [MND-013]
---

# MND-040 — iOS app foundation, design system and API client

**Why:** Every iOS feature task builds on this shell: navigation, theme from the Navy & Coral tokens, and the generated API client.

Epic `IOS` · PRD F10 · Size M (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-013

## Read first

- [docs/lld/ios.md](../../docs/lld/ios.md)
- [packages/design-tokens/tokens.json](../../packages/design-tokens/tokens.json)
- [packages/contracts/openapi.yaml](../../packages/contracts/openapi.yaml)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] Xcode project + SPM packages per docs/lld/ios.md (MandiDesign, MandiAPI, MandiCore, Feature*).
- [ ] Style Dictionary build generating Tokens.swift from packages/design-tokens; Sora font bundled; components PillButton, NavyHeroCard, GradePill, StoreBadge, PillTabBar.
- [ ] MandiAPI via swift-openapi-generator with auth middleware (single-flight refresh), Idempotency-Key and traceparent.
- [ ] fastlane lanes test and beta; GitHub Actions macOS workflow.

## Acceptance criteria

- [ ] The app launches to a placeholder Home using the design system on a iOS device.
- [ ] Changing a colour in tokens.json and rebuilding updates the app theme.
- [ ] A sample authenticated call succeeds against the local API.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-040: iOS app foundation, design system and API client` with acceptance criteria ticked.
