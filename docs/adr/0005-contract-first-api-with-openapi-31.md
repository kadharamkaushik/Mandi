# ADR-0005: Contract-first API with OpenAPI 3.1

Status: accepted · Date: 2026-09-27

## Decision

packages/contracts/openapi.yaml is the source of truth; server validation and both mobile clients are generated from it.

## Why

Three codebases (API, iOS, Android) built partly by parallel agents need one unambiguous contract. Spectral lints the spec in CI; breaking changes need a new version path.

## Consequences

Generators: swift-openapi-generator (iOS), openapi-generator kotlin + Retrofit (Android), openapi-typescript for server types.
