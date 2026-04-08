<div align="center">

# 🌸 @neelegirly/wa-api 🌸

### *Glow-up Multi-Session Wrapper fuer WhatsApp Web*  
### *QR-Love · Pairing Magic · Event Hooks · Stable Sessions*

[![npm](https://img.shields.io/npm/v/@neelegirly/wa-api?style=for-the-badge&color=ff69b4&logo=npm)](https://www.npmjs.com/package/@neelegirly/wa-api)
[![baileys](https://img.shields.io/badge/baileys-2.2.17-ff8fab?style=for-the-badge)](https://www.npmjs.com/package/@neelegirly/baileys)
[![libsignal](https://img.shields.io/badge/libsignal-1.0.28-f4a261?style=for-the-badge)](https://www.npmjs.com/package/@neelegirly/libsignal)
[![downloader](https://img.shields.io/badge/downloader-0.1.63-c77dff?style=for-the-badge)](https://www.npmjs.com/package/@neelegirly/downloader)

<p align="center">
  <img src="https://files.catbox.moe/c5adb6.jpeg" width="420" alt="Neelegirly wa-api hero" />
</p>

**💖 Release-Stack:** `@neelegirly/wa-api 1.7.16` · `@neelegirly/baileys 2.2.17` · `@neelegirly/libsignal 1.0.28` · `@neelegirly/downloader 0.1.63`

</div>

> `@neelegirly/wa-api` ist der schicke Multi-Session-Wrapper ueber `@neelegirly/baileys`: QR-Login, Pairing-Code-Flow, Session-Lifecycle, Messaging und Event-Hooks in einer kompakten API.

## ✨ Highlights

| Feature | Beschreibung | Status |
| --- | --- | --- |
| 💫 Multi-Session | mehrere Sessions gleichzeitig mit eigener Storage-Struktur | ✅ |
| 📷 QR-Flow | QR-Updates per Callback und optionale Terminal-Ausgabe | ✅ |
| 🔐 Pairing-Code | fester Pairing-Flow fuer Host-/Geräte-Login | ✅ |
| 💾 Session-Hardening | Credential-Saves werden gebuendelt und gezielt geflusht | ✅ |
| 🔔 Update-Hinweis | npm zuerst, GitHub-Fallback fuer neue Wrapper-Versionen | ✅ |
| 🎀 Event Hooks | `onConnected`, `onDisconnected`, `onMessageReceived` & mehr | ✅ |

## 📦 Kompatibilitaet

| Paket | Empfohlene Version |
| --- | --- |
| `@neelegirly/wa-api` | `1.7.16` |
| `@neelegirly/baileys` | `2.2.17` |
| `@neelegirly/libsignal` | `1.0.28` |
| `@neelegirly/downloader` | `0.1.63` |

Nur dieser exakt gepinnte Stack ist fuer den aktuellen Release vorgesehen.

## 🚀 Installation

```bash
npm install @neelegirly/wa-api@1.7.16 @neelegirly/baileys@2.2.17 @neelegirly/libsignal@1.0.28 @neelegirly/downloader@0.1.63 --save-exact
```

## ⚡ Quickstart

```js
const wa = require('@neelegirly/wa-api')

async function boot() {
  await wa.startSession('session-main', {
    printQR: true
  })
}

wa.onQRUpdated(({ sessionId, qr }) => {
  console.log(`QR aktualisiert fuer ${sessionId}:`, qr?.slice(0, 24) || 'leer')
})

wa.onConnected((sessionId) => {
  console.log(`Session verbunden: ${sessionId}`)
})

wa.onMessageReceived(async (msg) => {
  const text = msg.message?.conversation || msg.message?.extendedTextMessage?.text || ''
  const jid = msg.key?.remoteJid

  if (!jid) return

  if (text.toLowerCase() === 'ping') {
    await wa.sendMessage(msg.sessionId, jid, { text: 'pong 💖' })
  }
})

boot().catch(console.error)
```

## 🩷 Session-Glow-Up

- Credential-Saves werden **gebuendelt**, statt jeden einzelnen `creds.update` sofort auf die Platte zu schreiben.
- Bei `connection.open` und `connection.close` wird ein **Flush** erzwungen.
- Bereits gespeicherte Sessions koennen weiter ueber `loadSessionsFromStorage()` geladen werden.
- Der Wrapper setzt Branding-Kontext fuer QR-/Versionsanzeigen im Neelegirly-Stack.

## 🧩 API-Ueberblick

- `startSession(sessionId, { printQR })`
- `startSessionWithPairingCode(sessionId, { phoneNumber })`
- `getAllSession()`
- `getSession(sessionId)`
- `deleteSession(sessionId)`
- `loadSessionsFromStorage()`
- `sendMessage(sessionId, jid, content, options)`
- `onMessageReceived(listener)`
- `onMessageUpdate(listener)`
- `onQRUpdated(listener)`
- `onConnected(listener)`
- `onDisconnected(listener)`
- `onConnecting(listener)`
- `onPairingCode(listener)`

## 🔄 Versionshinweis

- Update-Check nutzt npm fuer `@neelegirly/wa-api` und GitHub Releases (`neelegirly/wa-api`) als Fallback.
- `@neelegirly/baileys` und `@neelegirly/libsignal` bleiben absichtlich exakt gepinnt.
- `@neelegirly/downloader` bleibt im Release-Stack exakt auf `0.1.63`.

## ⚠️ Hinweis

Dieses Projekt ist nicht offiziell mit WhatsApp oder Meta verbunden.
