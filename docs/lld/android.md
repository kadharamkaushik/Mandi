# LLD — Android app

Kotlin 2 · Jetpack Compose (Material 3 as base, custom Navy & Coral theme) · minSdk 26, targetSdk 35 · Gradle Kotlin DSL with version catalog. Decision record: [ADR-0001](../adr/0001-fully-native-ios-and-android-apps.md).

## Project layout (`apps/android`)

```
app/                         Application, MainActivity, navigation graph, Hilt setup
core/designsystem/           tokens generated from packages/design-tokens, components (PillButton, NavyHeroCard, GradePill, StoreBadge, PillNavBar)
core/network/                generated Retrofit client (openapi-generator, kotlinx.serialization), auth interceptor + authenticator
core/data/                   repositories, Room database (usuals, last plan), DataStore (settings)
core/model/                  domain models, money formatting
feature/onboarding|home|usuals|search|basket|checkout|orders|profile|insights/
build-logic/                 convention plugins
```

## Architecture

- MVVM with unidirectional data flow: `ViewModel` exposes `StateFlow<UiState>`; Compose screens are stateless; Hilt for DI; Kotlin coroutines everywhere.
- Navigation Compose with type-safe routes; app links (`https://mandi.app/...`) routed to screens.
- Networking: OkHttp interceptors for auth, idempotency keys and `traceparent`; an `Authenticator` refreshes once on 401 with a mutex.
- Storage: tokens in EncryptedSharedPreferences backed by Android Keystore (or DataStore + Tink); Room for offline Home.

## Platform features

| Need | Android approach |
| --- | --- |
| Store OAuth link | Custom Tabs; API HTTPS redirect returns to the app via a verified App Link |
| Tier C hand-off checklist | Conversation-style notification **bubble** (Android 11+) showing the checklist while the user is in the store app; a sticky notification on Android 8–10. No `SYSTEM_ALERT_WINDOW` and no accessibility service |
| Opening store apps | `Intent.ACTION_VIEW` on the store's app link; fall back to the web URL |
| Basket-due push | FCM data message → local notification with "Review basket" action |
| OTP autofill | SMS User Consent API |
| Background work | WorkManager for refreshes and pending confirmations |

## Quality

- Unit tests for ViewModels with Turbine; Compose UI tests; screenshot tests with Roborazzi.
- Maestro smoke flows shared with iOS.
- Baseline profile for startup; R8 full mode.
- Accessibility: TalkBack labels, 48 dp targets, font scaling to 200%.
- Play Data safety form and target API compliance maintained in MND-059.
