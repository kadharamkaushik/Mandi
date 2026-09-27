# LLD — Infrastructure (AWS, open source)

Region `ap-south-1` (Mumbai) for everything that stores personal data. Decision record: [ADR-0003](../adr/0003-aws-with-open-source-components.md).

## Accounts

AWS Organizations with accounts `mandi-shared` (ECR, DNS, CI roles), `mandi-dev`, `mandi-staging`, `mandi-prod`. GitHub Actions assumes roles through OIDC; no long-lived keys.

## OpenTofu layout (`infra/tofu`)

```
modules/ network, eks, rds-postgres, valkey, s3, kms, ecr, dns, observability
envs/    dev/ staging/ prod/   (each: main.tf, variables.tf, backend in S3 + DynamoDB lock)
```

## Network

One VPC per environment, 3 AZs, private subnets for EKS nodes and data stores, public subnets only for the load balancer, NAT gateways (one in dev, three in prod), VPC endpoints for S3, ECR, KMS, Secrets Manager.

## Compute (EKS)

| Piece | Choice |
| --- | --- |
| Cluster | Amazon EKS 1.31+, managed node group for system pods, Karpenter for workloads (Graviton `m7g`/`c7g`) |
| Ingress | Envoy Gateway (Gateway API) behind an AWS NLB; cert-manager with Let's Encrypt or ACM |
| GitOps | Argo CD app-of-apps from `infra/k8s` |
| Secrets | External Secrets Operator reading AWS Secrets Manager |
| Policy | Kyverno baseline policies (non-root, resource limits, signed images via cosign) |
| Autoscaling | HPA on CPU and on BullMQ queue depth (KEDA) for workers |

Workloads: `api` (min 2 replicas), `workers` (min 1, KEDA-scaled), `unleash`, observability stack.

## Data stores

| Store | Choice | Settings |
| --- | --- | --- |
| PostgreSQL | Amazon RDS for PostgreSQL 16, Multi-AZ in prod | PostGIS, pg_trgm, pgvector, pg_partman; PITR 7 days (prod 35); IAM auth for migrations |
| Valkey | Amazon ElastiCache for Valkey 8 | Cluster mode off at launch; TLS + AUTH |
| Object storage | S3 | Buckets `feeds-raw` (90-day lifecycle), `exports` (7-day), `assets`; SSE-KMS |
| Keys | AWS KMS | CMK for store-token data keys; separate CMK per environment |

## Observability

OpenTelemetry Collector (DaemonSet + gateway) → Prometheus (kube-prometheus-stack) for metrics, Loki for logs, Tempo for traces, Grafana for dashboards and alerts to Slack/PagerDuty. Dashboards: API RED, queue depth and failures, connector success by store and tier, plan accuracy, business KPIs from the PRD.

## CI/CD

- `services/*`: GitHub Actions — install, lint, typecheck, test (Testcontainers), build image, scan (Trivy), sign (cosign), push to ECR, bump Helm values; Argo CD syncs dev automatically, staging and prod by PR.
- `packages/contracts`: Spectral lint and breaking-change check (oasdiff) on every PR.
- `apps/ios`: fastlane on macOS runners — tests, build, TestFlight.
- `apps/android`: Gradle on Linux runners — tests, bundle, Play internal track.

## Local development

`docker compose up` starts PostgreSQL + PostGIS, Valkey, MinIO and Unleash; `pnpm dev` runs API and workers with `FakeStoreConnector`. Seed data: Bengaluru and Hyderabad pincodes, 200 products with offers for five stores.
