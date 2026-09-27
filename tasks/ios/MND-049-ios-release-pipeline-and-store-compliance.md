---
id: MND-049
title: "iOS release pipeline and store compliance"
epic: IOS
prd: F10
status: todo
owner: agent
size: S
depends_on: [MND-040]
---

# MND-049 — iOS release pipeline and store compliance

**Why:** Pilot users install through the platform's beta channel; store review needs accurate privacy disclosures.

Epic `IOS` · PRD F10 · Size S (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-040

## Read first

- [docs/lld/ios.md](../../docs/lld/ios.md)
- [docs/lld/infra.md#cicd](../../docs/lld/infra.md#cicd)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] Privacy manifest (PrivacyInfo.xcprivacy) and App Store privacy labels.
- [ ] TestFlight internal and external groups for the pilot.
- [ ] App Store review notes explaining store linking and hand-off.
- [ ] Crash reporting (open-source Sentry self-hosted or equivalent) and release notes template.

## Acceptance criteria

- [ ] A tagged build reaches the beta channel from CI without manual steps.
- [ ] Privacy disclosures match the data actually collected (checked against docs/analytics-events.md).

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-049: iOS release pipeline and store compliance` with acceptance criteria ticked.
