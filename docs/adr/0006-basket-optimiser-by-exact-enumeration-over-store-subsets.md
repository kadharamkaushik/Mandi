# ADR-0006: Basket optimiser by exact enumeration over store subsets

Status: accepted · Date: 2026-09-27

## Decision

For each subset of available stores (at most 2^N with N ≤ 8), assign each item to its cheapest in-stock offer within the subset, add each store's fees for its subtotal, apply the tap penalty, and keep the best plans.

## Why

Baskets have 5–30 items and a household sees at most 5–8 stores, so exact enumeration (≤ 256 subsets) runs in a few milliseconds and is easy to test and explain. Minimum order values and small-cart fees are handled per subset.

## Consequences

A MILP solver (HiGHS) can replace it if store counts grow; the module interface does not change.
