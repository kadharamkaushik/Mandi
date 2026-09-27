# @mandi/contracts

`openapi.yaml` is the single source of truth for the Mandi API (ADR-0005). It is a starter: task MND-013 completes it to cover every endpoint in [docs/lld/api.md](../../docs/lld/api.md).

- Lint: `pnpm --filter @mandi/contracts lint`
- Server types: `pnpm --filter @mandi/contracts generate`
- iOS client: swift-openapi-generator plugin in `apps/ios/Packages/MandiAPI` reads this file.
- Android client: openapi-generator (kotlin, retrofit2, kotlinx_serialization) in `apps/android/core/network`.
