# ADR-0008: PostgreSQL search before OpenSearch

Status: accepted · Date: 2026-09-27

## Decision

Product search uses PostgreSQL (tsvector + pg_trgm, pgvector for synonyms) for the MVP.

## Why

Catalogue size at launch is tens of thousands of products in two cities; one database is simpler to run and keeps search consistent with prices.

## Consequences

Move to OpenSearch when p95 search latency exceeds 150 ms or the catalogue passes 2 million store products.
