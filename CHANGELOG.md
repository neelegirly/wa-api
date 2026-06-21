# Changelog

## v1.8.12

### 🔗 Fix: dependency pin so a clean install pulls the WFTM fix

- Bumped declared `@neelegirly/baileys` dependency (and matching override) 2.2.26 → **2.2.28**.
- Identical code to 1.8.11; `npm install @neelegirly/wa-api` now transitively resolves baileys 2.2.28 → libsignal 1.0.33.

## v1.8.11

### 🔌 Wire persistent getMessage + retry config into the socket

- The socket now passes `getMessage`, `msgRetryCounterCache` and `cachedGroupMetadata`
  from `global.__neelegirlyWa` into Baileys, plus `maxMsgRetryCount: 5` and
  `retryRequestDelayMs: 2000`.
- Lets a host app supply a persistent plaintext store so incoming retry receipts can be
  answered even after a restart — the wa-api side of the "Waiting for this message" fix
  (pairs with baileys **2.2.27**'s `sendMessagesAgain` fallback).

## v1.8.10

### 🛠️ QR-/Pairing-Login-Fix + Modern Boot-Banner

- Aligned with `@neelegirly/baileys@2.2.26` (QR/pairing `405` fix + self-healing WA-Web version).
- Boot banner now shows the active WhatsApp-Web baseline (`2.3000.1035194821 · QR/Pair self-healing`).
- Dependency pin bumped to `@neelegirly/baileys@2.2.26`.

## v1.8.8-ecosystem-clean

### 💖 Neelegirly Ecosystem Clean Stability Update

- Removed workspace/core confusion from documentation.
- Clarified the 4-package architecture.
- Clarified that PM2 only runs the app.
- Clarified that WA-API handles sessions internally.
- Improved beginner-facing usage documentation.
