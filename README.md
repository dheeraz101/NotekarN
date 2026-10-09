<div align="center">

# 📢 NoteKar Remote Notices & Bulletins

[![Feed Status](https://img.shields.io/badge/Feed-Active-248A3D.svg?style=flat-square)](notification.json)
[![Platform Target](https://img.shields.io/badge/Targets-Android%20%7C%20PWA-0070F3.svg?style=flat-square)](notification.json)
[![Privacy](https://img.shields.io/badge/Privacy-Read--Only%20Feed-brightgreen.svg?style=flat-square)](https://notekarapp.vercel.app/privacy.html)
[![License: MIT](https://img.shields.io/badge/License-MIT-EAB308.svg?style=flat-square)](LICENSE)

### *Public Read-Only Broadcast Feed for NoteKar Applications*

**Zero Telemetry • Anonymous ETag Polling • Zero Device Identifiers • 100% Transparent**

</div>

---

## 🧭 What is this Repository?

This repository hosts the canonical public, read-only remote notice feed (`notification.json`) for:
1. **[NoteKar Android](https://github.com/dheeraz101/Notekar-Android)**
2. **[NoteKar Web PWA](https://github.com/dheeraz101/Notekar)**

It is used exclusively to publish emergency security bulletins, major version migration alerts, and important community announcements to installed clients.

---

## 🔒 Privacy & Security Model

- **Zero Egress / No Identifiers**: NoteKar clients poll this public raw GitHub URL anonymously. No user IDs, device hashes, IP records, or usage telemetry are ever transmitted or recorded.
- **Read-Only Static JSON**: This repository only contains static JSON configuration and documentation.
- **Client-Side Validation**: All notice evaluations (version bounds, expiration dates, display cooldowns, and platform matching) are computed 100% locally on user devices.

---

## 📄 Feed Schema & Documentation

- 📱 **Android Client Guide**: [`notification's guide(GAndroid).md`](notification's%20guide(GAndroid).md)
- 🌐 **Web PWA Client Guide**: [`notification's guide(pwa).md`](notification's%20guide(pwa).md)
- 📋 **Example Notice Payload**: [`notification-example(android).json`](notification-example(android).json)

---

## 📄 License

Distributed under the **[MIT License](LICENSE)**. Maintained by [Dheeraz](https://github.com/dheeraz101).
