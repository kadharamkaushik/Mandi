---
id: MND-002
title: "Network and EKS cluster with Karpenter, Envoy Gateway and Argo CD"
epic: PLAT
prd: F10
status: todo
owner: agent
size: L
depends_on: [MND-001]
---

# MND-002 — Network and EKS cluster with Karpenter, Envoy Gateway and Argo CD

**Why:** All services run on EKS. This task provisions the dev cluster end to end so later tasks only add Helm releases.

Epic `PLAT` · PRD F10 · Size L (S ≈ 1–2 days, M ≈ 3–5, L ≈ 1–2 weeks) · Owner: agent

## Depends on

- MND-001

## Read first

- [docs/lld/infra.md#compute-eks](../../docs/lld/infra.md#compute-eks)
- [docs/lld/infra.md#network](../../docs/lld/infra.md#network)
- [AGENTS.md](../../AGENTS.md) — repo rules for every task

## Scope

- [ ] OpenTofu modules network (3 AZ VPC, private subnets, NAT, VPC endpoints) and eks (EKS 1.31+, system node group, Karpenter).
- [ ] Install via Argo CD app-of-apps in infra/k8s: Envoy Gateway, cert-manager, External Secrets Operator, Kyverno baseline, KEDA, metrics-server.
- [ ] Gateway with TLS for api.dev.mandi.app.
- [ ] Document kubectl access through AWS SSO.

## Acceptance criteria

- [ ] A sample echo service is reachable over HTTPS at the dev hostname.
- [ ] Karpenter provisions Graviton nodes for a pending pod within 2 minutes.
- [ ] Kyverno blocks a pod that runs as root.

## Definition of done

- [ ] Code, tests and docs for this task only; unrelated changes go in a new task.
- [ ] Lint, typecheck and tests pass locally and in CI.
- [ ] Any change to the API goes through packages/contracts/openapi.yaml first.
- [ ] Docs in `docs/` updated where the design changed.
- [ ] Front matter `status` updated and `python3 tasks/index.py` rerun.
- [ ] Pull request titled `MND-002: Network and EKS cluster with Karpenter, Envoy Gateway and Argo CD` with acceptance criteria ticked.
