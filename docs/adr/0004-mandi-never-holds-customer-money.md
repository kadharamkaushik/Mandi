# ADR-0004: Mandi never holds customer money

Status: accepted · Date: 2026-09-27

## Decision

All orders are paid by the user directly to the store, either through the store's API with the user's saved method (tier A) or inside the store's app (tier C).

## Why

Collecting payment for other merchants' orders would make Mandi a payment aggregator under RBI rules and add refund liability.

## Consequences

When NPCI's agent-payment protocol launches, pre-authorised payments still flow user to store; Mandi only orchestrates.
