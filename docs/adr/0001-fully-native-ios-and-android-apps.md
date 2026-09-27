# ADR-0001: Fully native iOS and Android apps

Status: accepted · Date: 2026-09-27

## Decision

Build the iOS app in Swift/SwiftUI and the Android app in Kotlin/Jetpack Compose, with no shared runtime code.

## Why

The hand-off experience depends on platform-only features (iOS Live Activities, Android notification bubbles, custom tabs, universal/app links). Separate native codebases let Cowork agents work on each app in parallel without a shared build. Duplication is contained by generating both API clients from one OpenAPI contract and both themes from one token file.

## Consequences

Business rules (plan totals, grades) stay on the server so the apps only render. Kotlin Multiplatform was considered and rejected for now: it would couple the two app builds and slow parallel work.
