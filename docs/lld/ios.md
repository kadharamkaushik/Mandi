# LLD — iOS app

Swift 6 (strict concurrency) · SwiftUI · iOS 17.0+ · Xcode 16+ · Swift Package Manager only. Decision record: [ADR-0001](../adr/0001-fully-native-ios-and-android-apps.md).

## Project layout (`apps/ios`)

```
Mandi.xcodeproj
Mandi/                     app target: App entry, DI container, root navigation
Packages/
  MandiDesign/             tokens generated from packages/design-tokens, components (PillButton, NavyHeroCard, GradePill, StoreBadge, PillTabBar)
  MandiAPI/                generated client (swift-openapi-generator) + auth middleware
  MandiCore/               domain models, formatting (₹ in paise), feature flags
  Feature*/                one package per feature: Onboarding, Home, Usuals, Search, Basket, Checkout, Orders, Profile, Insights
MandiLiveActivity/         widget extension: hand-off checklist Live Activity
MandiTests/, MandiUITests/
```

## Architecture

- MVVM with the Observation framework: each screen has an `@Observable` view model with `async` intents; views are stateless.
- Navigation: one `NavigationStack` per tab with typed routes; a `Router` handles deep links.
- Networking: `MandiAPI` client with middleware for auth (attach access token, refresh once on 401 with single-flight), `Idempotency-Key` on POSTs, `traceparent`.
- Storage: tokens in Keychain (`kSecAttrAccessibleAfterFirstUnlockThisDeviceOnly`); small caches with SwiftData (usuals, last plan) for instant Home.
- Money and units come pre-computed from the API; the app never recomputes totals.

## Platform features

| Need | iOS approach |
| --- | --- |
| Store OAuth link | `ASWebAuthenticationSession` with `prefersEphemeralWebBrowserSession = false`; callback via the API's HTTPS redirect then a universal link back to the app |
| Tier C hand-off checklist | Live Activity (ActivityKit) on Lock Screen and Dynamic Island showing store, next item, quantity and progress; updated by the app and by push (`liveactivity` token) as the user ticks items |
| Opening store apps | Universal links from the API's `open_url`; `UIApplication.open` with fallback to web URL |
| Basket-due push | APNs with actionable notification ("Review basket"); opens the confirm sheet directly |
| OTP autofill | `textContentType(.oneTimeCode)` |
| Location | Core Location, when-in-use only, for address pin |

iOS cannot draw over other apps; the Live Activity is the checklist equivalent of Android's bubble.

## Screens (from the design canvas, Navy & Coral)

Onboarding (6), Home with navy summary card, Pay/confirm sheet, placing orders, order done and detail, MVP hand-off flow (plan choice, check out per store, confirm), Search (4), My List, Edit usual, Pause, Insights, Profile (5).

## Quality

- Unit tests for view models with a fake API; snapshot tests for design components (swift-snapshot-testing).
- UI smoke tests with Maestro flows shared with Android where possible.
- Accessibility: Dynamic Type up to XXL, VoiceOver labels on every control, 44 pt targets.
- Privacy manifest (`PrivacyInfo.xcprivacy`) and App Store privacy labels maintained in MND-049.
