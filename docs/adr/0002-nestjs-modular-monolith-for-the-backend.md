# ADR-0002: NestJS modular monolith for the backend

Status: accepted · Date: 2026-09-27

## Decision

One NestJS API deployable plus one workers deployable, organised as modules with enforced boundaries.

## Why

The team and agents need one codebase to reason about; traffic at launch (tens of requests per second) does not justify microservices. Modules (identity, users, stores, catalog, usuals, baskets, checkout, orders, health, notifications) talk through their public services only; eslint boundary rules block deep imports.

## Consequences

Any module can later be extracted behind the same interface. TypeScript was chosen over Kotlin for hiring breadth and iteration speed.
