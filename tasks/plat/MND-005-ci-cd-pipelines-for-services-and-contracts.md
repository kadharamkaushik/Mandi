---
id: MND-005
title: "CI/CD pipelines for services and contracts"
epic: PLAT
prd: F10
status: todo
owner: agent
size: M
depends_on: [MND-001, MND-010]
---

# MND-005 — CI/CD pipelines for services and contracts

**Why:** Every merge to main should build, test, scan, sign and deploy services to dev automatically.

Epic `PLAT` · PRD F10 · Size M (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-001
- MND-010

## Read first

- [docs/lld/infra.md#cicd](../../docs/lld/infra.md#cicd)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] .github/workflows/services.yml: pnpm install, lint, typecheck, test (Testcontainers), build images, Trivy scan, cosign sign, push to ECR, update Helm values in infra/k8s.
- [ ] .github/workflows/contracts.yml: Spectral lint and oasdiff breaking-change check.
- [ ] Argo CD: dev auto-sync; staging and prod via PR to their values files.
- [ ] Branch protection: required checks listed in AGENTS.md.

## Acceptance criteria

- [ ] A PR that breaks the OpenAPI contract fails CI with the oasdiff report.
- [ ] Merging to main deploys api and workers to dev within 15 minutes.
- [ ] Images in ECR are signed and verifiable with cosign.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-005: CI/CD pipelines for services and contracts` with acceptance criteria ticked.
