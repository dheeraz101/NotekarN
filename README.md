<div align="center">

# 📢 NoteKar Remote Notices & Feature Bulletins

[![Feed Status](https://img.shields.io/badge/Feed-Active-248A3D.svg?style=flat-square)](notification.json)
[![Platform Target](https://img.shields.io/badge/Targets-Android%20%7C%20PWA-0070F3.svg?style=flat-square)](notification.json)
[![Privacy](https://img.shields.io/badge/Privacy-Zero--Tracking%20Guarantee-brightgreen.svg?style=flat-square)](https://notekarapp.vercel.app/privacy.html)
[![Release Channels](https://img.shields.io/badge/Channels-Stable%20%7C%20Priority%20%7C%20Beta%20%7C%20Experiment-orange.svg?style=flat-square)](notification.json)
[![License: MIT](https://img.shields.io/badge/License-MIT-EAB308.svg?style=flat-square)](LICENSE)

### *Public Read-Only Broadcast Feed & Interactive In-App Feature Showcase for NoteKar*

**Zero Telemetry • Anonymous ETag Polling • Zero Device Identifiers • 100% Transparent**

</div>

---

## 🧭 Overview & Capabilities

This repository hosts the canonical public, read-only remote feed (`notification.json`) consumed by **[NoteKar Android](https://github.com/dheeraz101/Notekar-Android)** and **[NoteKar Web PWA](https://github.com/dheeraz101/Notekar)**.

The feed powers two distinct systems inside NoteKar:
1. **Critical Advisories & Security Alerts**: Emergency alerts for bug mitigations, database migrations, or urgent patch releases.
2. **Official Bulletins & Feature Showcase**: A dedicated in-app feature feed (inspired by WhatsApp status updates) designed to showcase new features, widgets, and capabilities directly in NoteKar without spamming system push notifications.

---

## 🚀 Official Bulletins & Feature Showcase Mode

Unlike standard push notifications that distract users on their device lock screens, **Feature Showcase Bulletins** (`priority: "feature"`) are designed specifically for the in-app Official Bulletins page:
- **No Background Push Spam**: Feature bulletins do not display noisy heads-up system notifications; they appear elegantly inside the in-app **Official Bulletins** feed.
- **Rich Visual Spotlight**: Highlighted with emerald green badges (`FEATURE`), clear titles, multi-language descriptions, and dedicated action pills.
- **Direct Deep-Link Navigation**: Tapping an action button can take the user directly to any screen, composer, or settings subpage inside NoteKar.

### Supported In-App Deep-Link Actions

| Action Identifier | Destination in NoteKar |
| :--- | :--- |
| `page:sobriety` or `sobriety` | Opens Sobriety Companion settings & streak details |
| `page:audit` or `audit` | Opens Life Audit & intentionality analytics |
| `page:history` or `history` | Opens the full history timeline & search |
| `page:plus_note` or `plus_note` | Opens the Plus Note bottom composer |
| `page:backup` or `backup` | Opens Data & Backup management page |
| `page:camera` or `camera` | Launches the Instant Camera photo capture logger |
| `settings:<Category Name>` | Deep-links directly to any settings subcategory (e.g. `settings:App Update Center`) |
| `https://...` | External web URL (prompts confirmation alert before launching) |

---

## 📦 Release Channels & Versioning Architecture

NoteKar supports four distinct release tiers to accommodate stability and rapid innovation:

```
+-------------------------------------------------------------------------------+
|                           NOTEKAR RELEASE TIERS                               |
+-------------------------------------------------------------------------------+
| 1. Stable Release (SR)       | Production-ready, fully verified milestone.    |
|    Format: x.y.z             | e.g. 8.0.0                                     |
+------------------------------+------------------------------------------------+
| 2. Priority Release (PR)     | Rapid stabilization & critical engine patches. |
|    Format: x.y.0             | e.g. 8.1.0                                     |
+------------------------------+------------------------------------------------+
| 3. Beta Release (BR)         | Public feature previews for testers.           |
|    Format: x.y.z             | e.g. 8.1.1                                     |
+------------------------------+------------------------------------------------+
| 4. Experimental Release (ER) | Bleeding-edge features; high-risk early tests. |
|    Format: x.y.zE[n]         | e.g. 8.1.1E1, 8.1.1E2 (resets to E1 on base)   |
+-------------------------------------------------------------------------------+
```

### Versioning Rules:
- **Comprehensive Update Distribution**: The Experiment release channel receives **ALL updates across all channels** (Stable, Priority, Beta, and Experiment). Whenever an update is published on any channel, users subscribed to Experiment receive it immediately.
- **ER (Experimental Release)**: Appends `E1`, `E2`, etc. to the current base version. For example, if the current base version is `8.0.0`, experimental builds are numbered `8.0.0E1`, `8.0.0E2`. If a new beta or priority release bumps to `8.1.0`, subsequent experimental builds increment from `8.1.0E1`.
- **High-Alert Guardrail Modal**: When a user selects the Experiment track in Settings -> App Update Center, NoteKar presents an Apple HIG high-visibility red modal disclosing all risks and offering three choices:
  1. `Backup First`: Exports a complete offline JSON backup before switching.
  2. `Cancel`: Keeps existing channel preference.
  3. `I Agree`: Confirms channel switch to experimental updates.

---

## 📄 Notice JSON Schema Specification

Each bulletin or notice in `notification.json` is a JSON object with the following fields:

```json
{
  "id": "unique-slug-identifier",
  "enabled": true,
  "title": "Default English Title",
  "title_es": "Título en español",
  "title_hi": "हिंदी शीर्षक",
  "title_de": "Deutscher Titel",
  "title_fr": "Titre français",
  "title_ja": "日本語タイトル",
  "title_ru": "Русский заголовок",
  "body": "Detailed description of the feature or notice in English.",
  "body_es": "Descripción en español.",
  "body_hi": "हिंदी विवरण।",
  "body_de": "Beschreibung auf Deutsch.",
  "body_fr": "Description en français.",
  "body_ja": "日本語での説明。",
  "body_ru": "Описание на русском языке.",
  "url": "notekar://sobriety",
  "action": "page:sobriety",
  "priority": "feature",
  "channels": ["stable", "beta", "experiment"],
  "platforms": ["android"],
  "minVersion": "8.0.0",
  "maxVersion": "8.9.9",
  "maxShows": 5,
  "cooldownHours": 48,
  "startsAt": "2026-10-01T00:00:00Z",
  "expiresAt": "2027-01-01T00:00:00Z"
}
```

### Field Definitions:

| Property | Type | Description |
| :--- | :--- | :--- |
| `id` | `String` | Unique bulletin identifier used for local caching and display counts. |
| `enabled` | `Boolean` | Toggles whether client devices should evaluate and display this bulletin. |
| `title` | `String` | Main English title. Localized titles (`title_es`, `title_hi`, etc.) are displayed automatically based on system locale. |
| `body` | `String` | Primary descriptive content. Supports localized equivalents (`body_es`, `body_hi`, etc.). |
| `priority` | `String` | Categorizes the notice: `"critical"` (red advisory), `"security"` (purple advisory), `"feature"` (green spotlight showcase), `"normal"` (standard release bulletin), or `"low"` (curated tip). |
| `action` | `String` | In-app deep link target (e.g. `page:sobriety`, `settings:App Update Center`, `page:plus_note`) or `"releases"`. |
| `url` | `String` | Fallback URL or external link (`https://...`). Tapping opens the safe departure confirmation dialog. |
| `channels` | `Array<String>` | Targeted release channels: `["stable"]`, `["beta"]`, `["experiment"]`, or combinations thereof. |
| `platforms` | `Array<String>` | Target client platform: `["android"]`, `["pwa"]`. |
| `minVersion` / `maxVersion` | `String` | Optional semver bounds (e.g. `minVersion: "8.0.0"`). Omit to target all versions. |
| `maxShows` | `Integer` | Maximum number of times the notice may be displayed to an individual client. |
| `cooldownHours` | `Integer` | Minimum cooldown hours required between consecutive displays. |
| `startsAt` / `expiresAt` | `ISO 8601 String` | Optional time windows during which the bulletin is active. |

---

## 🔒 Privacy & Security Model

- **Zero Egress / Zero Identifiers**: NoteKar clients poll this public raw GitHub JSON URL anonymously using standard HTTP conditional `GET` headers (`If-None-Match`).
- **Zero Device Telemetry**: No user IDs, IMEI numbers, advertising IDs, device fingerprints, or IP records are ever gathered, stored, or transmitted.
- **Client-Side Validation**: All evaluations (version constraints, channel matching, cooldown calculation) execute 100% offline and locally inside the NoteKar app.

---

## 📄 License

Distributed under the **[MIT License](LICENSE)**. Maintained by [Dheeraz](https://github.com/dheeraz101).
