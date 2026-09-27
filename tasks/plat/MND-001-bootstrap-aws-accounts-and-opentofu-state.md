---
id: MND-001
title: "Bootstrap AWS accounts and OpenTofu state"
epic: PLAT
prd: F10
status: todo
owner: human+agent
size: M
depends_on: []
---

# MND-001 — Bootstrap AWS accounts and OpenTofu state

**Why:** Nothing can be deployed until the AWS organisation, accounts and a remote state backend exist. A human with billing access creates the organisation; an agent writes the OpenTofu code.

Epic `PLAT` · PRD F10 · Size M (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: human+agent

## Depends on

- Nothing; can start now.

## Read first

- [docs/lld/infra.md#accounts](../../docs/lld/infra.md#accounts)
- [docs/adr/0003-aws-with-open-source-components.md](../../docs/adr/0003-aws-with-open-source-components.md)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] Create AWS Organizations with accounts mandi-shared, mandi-dev, mandi-staging, mandi-prod (human).
- [ ] infra/tofu/bootstrap: S3 state bucket + DynamoDB lock table per account, KMS key for state.
- [ ] GitHub OIDC provider and deploy roles (least privilege) in each account.
- [ ] infra/tofu/envs/{dev,staging,prod} skeletons with backend config and provider pinned to ap-south-1.

## Acceptance criteria

- [ ] `tofu plan` runs clean for dev from GitHub Actions using OIDC (no static keys).
- [ ] State bucket has versioning, SSE-KMS and public access block.
- [ ] README in infra/tofu explains how to add an environment.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-001: Bootstrap AWS accounts and OpenTofu state` with acceptance criteria ticked.
