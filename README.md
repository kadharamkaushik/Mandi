# Mandi

Mandi keeps each household's list of usual groceries, prices that basket across quick-commerce stores (Zepto, Swiggy Instamart, Blinkit, BB Now, FirstClub) with every fee included, and gets it into the cheapest set of carts in as few taps as each store allows.

- Product requirements: [docs/prd.md](docs/prd.md)
- High-level design: [docs/hld.md](docs/hld.md)
- Low-level designs: [docs/lld/](docs/lld/README.md)
- Architecture decisions: [docs/adr/](docs/adr/README.md)
- Implementation backlog: [tasks/INDEX.md](tasks/INDEX.md)
- Working in this repo (humans and agents): [AGENTS.md](AGENTS.md)

## Repository layout

| Path | What lives there | Stack |
| --- | --- | --- |
| `apps/ios` | iOS app | Swift 6, SwiftUI, iOS 17+, Swift Package Manager |
| `apps/android` | Android app | Kotlin 2, Jetpack Compose, minSdk 26, Gradle KTS |
| `services/api` | Public API (modular monolith) | Node 22, TypeScript, NestJS 11, PostgreSQL, Valkey |
| `services/workers` | Background jobs (prices, matching, schedules, order polling) | NestJS standalone app + BullMQ |
| `packages/contracts` | OpenAPI 3.1 contract; source of truth for all clients | OpenAPI, Spectral, generators |
| `packages/design-tokens` | Navy & Coral design tokens for both apps | Style Dictionary |
| `infra/tofu` | AWS infrastructure as code | OpenTofu |
| `infra/k8s` | Kubernetes manifests and Helm values | Helm, Argo CD |
| `docs` | PRD summary, HLD, LLDs, ADRs | Markdown |
| `tasks` | Implementation tasks, one file each | Markdown |

## Launch scope

MVP launches in Bengaluru and Hyderabad. Zepto orders are placed directly (two taps); Instamart joins once Swiggy Builders Club access is approved; Blinkit, BB Now and FirstClub use a guided hand-off to their own apps.
