# Mandi infrastructure

AWS, built mostly from open-source components. Design: [docs/lld/infra.md](../docs/lld/infra.md).

- `tofu/` — OpenTofu modules and environments (`dev`, `staging`, `prod`) in `ap-south-1` (Mumbai).
- `k8s/` — Helm charts and Argo CD applications for EKS.
