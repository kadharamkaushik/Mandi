# LLD — Security and privacy

## Threat model (top risks)

| Threat | Control |
| --- | --- |
| Stolen store OAuth tokens | Envelope encryption with per-user KMS data keys; decrypt per call; KMS access only from API/worker IAM roles; token redaction in logs |
| Account takeover via OTP abuse | 5 attempts per challenge, 5 OTPs per phone per hour, device binding on refresh tokens, SIM-swap check via SMS provider where available |
| Unwanted orders placed on the user's behalf | Tier A orders always need an explicit confirm tap with the amount shown; idempotency keys; re-check before placement |
| Refresh-token theft | Rotation with reuse detection revoking the whole session family |
| Insecure mobile storage | Keychain / Android Keystore only; no tokens in logs, screenshots blocked on OTP screens |
| Supply chain | Renovate, lockfiles, Trivy scans, cosign-signed images, Kyverno admission |

Both apps follow OWASP MASVS L1; the API follows OWASP ASVS L2 for auth and session controls.

## DPDP Act 2023 and Rules 2025

- Consent notices per purpose (order-history import, email order detection, analytics, marketing) with versioned text; consent ledger in `consents`.
- Data principal rights: access and export (`POST /me/export`), correction (profile edit), erasure (`DELETE /me`, completed within 30 days, well inside the 90-day limit), grievance contact shown in Profile.
- Data minimisation: no contacts, no SMS reading, no precise background location; email access (P1) limited to order-confirmation senders.
- Breach response: runbook with user notification templates in plain language.
- Personal data stays in `ap-south-1`; processors (SMS gateway, push, analytics) listed in the privacy notice.
