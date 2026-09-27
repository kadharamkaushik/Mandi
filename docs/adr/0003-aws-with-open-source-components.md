# ADR-0003: AWS with open-source components

Status: accepted · Date: 2026-09-27

## Decision

Run on AWS in ap-south-1 using managed hosting for open-source engines, and open-source software for everything else.

## Why

Data residency in India, and no lock-in at the application layer. Choices: Amazon EKS (Kubernetes), RDS for PostgreSQL 16, ElastiCache for Valkey, S3, OpenTofu for IaC, Argo CD for GitOps, Envoy Gateway for ingress (Gateway API), Karpenter for node autoscaling, External Secrets Operator with AWS Secrets Manager, OpenTelemetry with Prometheus, Loki, Tempo and Grafana, Unleash for feature flags.

## Consequences

ingress-nginx is not used because the Kubernetes project has retired it. Every managed service used has a self-hostable open-source equivalent.
