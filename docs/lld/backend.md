# LLD — Backend (NestJS)

Two deployables from one pnpm workspace: `services/api` (HTTP) and `services/workers` (queues and schedules). Shared code lives in `packages/*` inside the workspace (`@mandi/domain`, `@mandi/connectors`, `@mandi/optimiser`, `@mandi/health`, `@mandi/db`).

## Stack

Node 22 LTS · TypeScript 5 (strict) · NestJS 11 with Fastify · Drizzle ORM + drizzle-kit migrations · BullMQ on Valkey · pino logging · OpenTelemetry SDK (auto-instrumentation for http, pg, ioredis) · Vitest + Testcontainers (PostgreSQL, Valkey) · ESLint with `eslint-plugin-boundaries` · Zod for config.

## Module layout (`services/api/src`)

```
main.ts                 bootstrap: Fastify, OTel, helmet, CORS off (mobile only), problem-details filter
config/                 Zod-validated env config
common/                 auth guard, idempotency interceptor, rate-limit guard, problem-details, pagination
modules/
  identity/             OTP, sessions, JWT, devices
  users/                profile, consents, export, deletion
  places/               addresses, serviceability
  stores/               store registry, capabilities, links, OAuth callbacks
  catalog/              search, product page, swaps
  usuals/               usuals CRUD, import, cadence, pause
  baskets/              current basket, plans (calls @mandi/optimiser)
  checkout/             router, re-check, tier A placement, tier C hand-off steps
  orders/               orders, confirmation, issues
  health/               health profile, grades (calls @mandi/health)
  insights/             monthly aggregates (P1)
  notifications/        device registry, send API used by workers
```

Rules: a module exposes one `*.service.ts` facade; other modules import only that facade (enforced by `eslint-plugin-boundaries`). Controllers are thin; validation comes from types generated from the OpenAPI spec (`openapi-typescript`) plus Zod schemas generated with `openapi-zod-client` or equivalent.

## Cross-cutting

- **Auth guard**: verifies EdDSA JWT with key id rotation (keys in Secrets Manager, cached 5 min). Public routes are opt-in with `@Public()`.
- **Idempotency interceptor**: stores `(user, route, key) → response` in `idempotency_keys` inside the same transaction as the side effect.
- **Transactional outbox**: domain events (`order.placed`, `usual.bought`, `store_link.created`) are written to `outbox` in the same transaction and relayed to BullMQ by the workers; no dual writes.
- **Errors**: one exception filter maps domain errors to RFC 9457 problems with stable `code`s.
- **Observability**: every request has a trace; spans for each connector call carry `store_id`, `tier`, `outcome`. RED metrics per route; business counters `plans_computed`, `orders_placed{store,tier}`, `handoff_confirmed{store}`.
- **Feature flags**: Unleash SDK; flags `instamart_tier_a`, `tier_b_cart_fill`, `insights`, `swaps`.

## Workers

| Queue / schedule | Trigger | Job |
| --- | --- | --- |
| `offers.refresh` | every 15 min per pincode cluster; on demand for stale items | Pull offers from feeds / tier A connectors, upsert `offers`, update Valkey hot cache |
| `fees.refresh` | daily 03:00 IST | Refresh `fee_rules` from sources; flag changes for review |
| `match.candidates` | new or changed `store_products` | Run matcher; auto-confirm ≥ 0.92, queue 0.75–0.92 for review |
| `usuals.import` | `store_link.created` event | Pull order history, build usuals with cadence |
| `usuals.due` | hourly | Set basket items for users with `next_due_on ≤ today + 1`; enqueue `notify.basket_due` at the user's preferred hour |
| `orders.poll` | every 60 s while a tier A order is not terminal | Update status via connector `orderStatus` |
| `notify.*` | events | Send APNs / FCM; record in `notifications` |
| `account.delete` | 30 days after request | Hard delete per data-model.md |
| `outbox.relay` | continuous | Move outbox rows to queues |

Each job is idempotent, has a max-attempt count with exponential backoff, and lands in a dead-letter queue with an alert after the last failure.

## Testing

- Unit: domain services and pure modules (`@mandi/optimiser`, `@mandi/health`) at 90%+ line coverage.
- Integration: Testcontainers for PostgreSQL + Valkey; connectors replaced by `FakeStoreConnector`.
- Contract: every controller response validated against the OpenAPI spec in tests.
- Golden files: optimiser plans for 30 fixed baskets checked into `packages/optimiser/test/golden`.
