# Working in the Mandi repo

Rules for every contributor, human or agent (Claude Cowork, Claude Code, Codex, etc.). Read this before starting any task.

## 1. Pick a task

1. Open [tasks/INDEX.md](tasks/INDEX.md) and choose one item from **Ready to pick up now** whose owner is `agent` (or `human+agent` if a human has done their part).
2. Set its front matter `status: in-progress`, run `python3 tasks/index.py`, and commit that change first so parallel sessions do not collide.
3. Work only inside the task's scope. If you discover extra work, add a new task file (next free `MND-` number in the right epic folder) instead of expanding scope.
4. When done: tick the task's checklists, set `status: in-review`, rerun `python3 tasks/index.py`, open a PR titled `MND-xxx: <title>`.

Parallel sessions: tasks in the same wave with no shared dependency can run at the same time. Never pick a task whose dependencies are not `done`.

## 2. Sources of truth (in this order)

1. `packages/contracts/openapi.yaml` — the API. Change the contract first, then the server and clients.
2. `docs/adr/*` — decisions. Do not contradict an ADR; propose a new one instead.
3. `docs/lld/*` — how each part works.
4. `docs/hld.md` and `docs/prd.md` — why and what.
5. `packages/design-tokens/tokens.json` — colours, type, spacing (Navy & Coral). Never hard-code colours in app code.

## 3. Stack and conventions

| Area | Rules |
| --- | --- |
| Backend | Node 22, TypeScript strict, NestJS 11 (Fastify), Drizzle, BullMQ on Valkey, Vitest + Testcontainers. Modules import each other only through their `*.service.ts` facade. Money is integer paise. |
| iOS | Swift 6 strict concurrency, SwiftUI, iOS 17+, SPM only, MVVM with `@Observable`. Tokens in Keychain. |
| Android | Kotlin 2, Compose, minSdk 26, Hilt, Retrofit (generated), Room. Tokens in Keystore-backed storage. |
| Infra | OpenTofu, EKS, Argo CD, Helm. Region `ap-south-1`. No console changes without code. |
| Commits | Conventional commits prefixed with the task id: `feat(MND-031): enumerate store subsets`. |
| Tests | Every task adds tests; pure packages (optimiser, health) keep ≥ 90% line coverage. |

## 4. Hard rules

- Mandi never collects or stores payment data (ADR-0004).
- Store access only through official APIs, contracted feeds or deep links. No scraping of logged-in sessions, no unofficial store wrappers, no automation of other apps (ADR-0007).
- Never log tokens, OTPs or full phone numbers. Use the shared pino redaction config.
- Personal data stays in `ap-south-1`.
- Secrets come from AWS Secrets Manager via External Secrets; never commit `.env` files.

## 5. Graphify

This repo uses [Graphify](https://graphify.net/) to keep a knowledge graph of code and docs in `graphify-out/` so agents can navigate by structure.

- One-time on your machine: `uv tool install graphifyy` then `graphify install` (registers the `/graphify` skill with your assistant).
- Build or refresh the full graph (code + docs) from an assistant session: `/graphify .`
- Code-only refresh without an LLM: `graphify update .`
- Ask the graph before grepping: `graphify query "how does checkout pick a tier?"`, `graphify path "CheckoutService" "StoreConnector"`, `graphify explain "optimiser"`.
- Keep it fresh automatically in your clone: `graphify hook install` (post-commit rebuild).
- Read `graphify-out/GRAPH_REPORT.md` first when you need the big picture.

Task MND-009 owns keeping the graph current in CI.
