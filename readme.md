<div align="center">

# @neelify/wa-api

### Multi-Session Wrapper fuer Baileys
### Session Manager · QR · Pairing Code · Message Helpers

[![Version](https://img.shields.io/badge/Version-1.7.1-ff69b4?style=for-the-badge&logo=github)](https://github.com/neelify/wa-api)
[![Companion](https://img.shields.io/badge/Companion-@neelify%2Fbaileys-9b59b6?style=for-the-badge)](https://www.npmjs.com/package/@neelify/baileys)
[![npm](https://img.shields.io/npm/v/@neelify/wa-api?style=for-the-badge&color=ff69b4&logo=npm)](https://www.npmjs.com/package/@neelify/wa-api)
[![Node](https://img.shields.io/badge/Node-16+-green?style=for-the-badge&logo=node.js)](https://nodejs.org)

---

<p align="center">
  <img src="https://files.catbox.moe/6np1ii.JPG" width="720" alt="Neelify wa-api Header" />
</p>

[**Installation**](#installation) · [**Quickstart**](#quickstart) · [**API-Hinweise**](#api-hinweise) · [**Changelog**](#changelog)

</div>

---

## Installation

```bash
npm install @neelify/wa-api@latest
```

```bash
yarn add @neelify/wa-api@latest
```

## Quickstart

```js
const WAApi = require('@neelify/wa-api')

const api = new WAApi({
  session: 'main',
  printQRInTerminal: true
})

api.on('ready', () => {
  console.log('wa-api ready')
})

api.on('message', async (msg) => {
  if (msg.text === 'ping') {
    await api.sendText(msg.from, 'pong')
  }
})
```

## API-Hinweise

- Wrapper ueber `@neelify/baileys` fuer einfachere Integrationen
- Multi-Session Verwaltung in einer gemeinsamen API
- Pairing-Code und QR Events fuer Login-Flows
- Message-Helper fuer typische Bot-Use-Cases

## Companion Packages

```bash
npm install @neelify/baileys @neelify/wa-api @neelify/libsignal
```

## Changelog

### 1.7.1

- README bereinigt und strukturiert
- Entfernt: lange numerierte Platzhalter-Bloecke
- Namespace-Referenzen auf `@neelify/*` vereinheitlicht

### 1.7.0

- Migration auf `@neelify/wa-api`

---

<div align="center">

Stay connected.

</div>

