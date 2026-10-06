# Changelog

## v1.8.15

### 🔁 Fix: Retry-Anfragen ohne Hooks scheiterten immer

- Seit 1.8.11 reichte `openSessionRuntime` `getMessage`, `msgRetryCounterCache` und `cachedGroupMetadata` aus
  `global.__neelegirlyWa` IMMER an den Socket — auch als `undefined`, wenn kein Hook gesetzt war. Per Spread
  überschrieb `getMessage: undefined` den Baileys-Standard `async () => undefined`; jede eingehende Retry-Anfrage
  endete mit `getMessage is not a function`, der Empfänger blieb auf „Warte auf diese Nachricht“. Betraf jeden
  Nutzer ohne eigene Hooks (im Feld: DarkBot). Jetzt werden nur gesetzte Hooks weitergereicht.

## v1.8.14

### 🔗 baileys 2.2.31 (Message Recovery & Decryption Stability)

- `@neelegirly/baileys` dependency + override → **2.2.31** (1.8.13 zeigte noch auf 2.2.29). 2.2.31 behebt die
  Hauptursachen für dauerhaftes „Warte auf diese Nachricht" (Gerät beim Entschlüsseln, Retry-Adressierung, LID/PN).

### 🧹 Kein fester Serverpfad mehr

- `openSessionRuntime` und die Legacy-Klasse in `dist/whatsapp/index.js` versuchten
  `require("/root/OniSelf/src/sessions/sqlite-auth-state.js")` — ein Pfad auf genau einem Rechner, der überall sonst still
  fehlschlug. Ersetzt durch den optionalen Hook `global.__neelegirlyWa.useAuthState(credentialDirectory, { sessionId })`
  → `{ state, saveCreds }`. Ohne Hook (oder wenn er fehlschlägt): baileys' Multi-File-Ablage wie bisher.

### 📦 Frische Installation lief nicht

- `dist/Messaging/index.js` lud `qrcode`, ohne es zu benutzen oder zu deklarieren → `Cannot find module 'qrcode'` bei
  jedem frischen `npm i @neelegirly/wa-api`. Zeile entfernt. (`better-sqlite3` bleibt optional, nur in `try/catch`.)

### ⏱️ QR-/Verbindungs-Zeitgrenzen durchreichbar

- `global.__neelegirlyWa.qrTimeout` / `.connectTimeoutMs` werden an den Socket gereicht. Baileys gibt sonst nur dem
  ersten QR-Code 60 s, jedem weiteren 20 s („QR refs attempts ended"). Ohne Hook: Baileys-Standard.

## v1.8.13

### 🔗 Bump baileys dependency to 2.2.29 (device-change fix)

- Declared `@neelegirly/baileys` dependency (and override) → **2.2.29** so a clean install pulls the instant device-change detection fix. Code identical to 1.8.12.

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
