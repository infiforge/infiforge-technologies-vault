---
date: 2026-04-29
tags:
  - area
  - frontend
  - flutter
  - mobile
---

# Frontend Development

## Focus

Frontend development for Infiforge services using Flutter and Riverpod with Consumables.

## Related Projects

All 11 services have Flutter frontends:
- [[Bliss — Hotel Management System]]
- [[Compete — School Management System]]
- [[Farmup — Farm Management System]]
- [[Hail — Skill Sharing Marketplace]]
- [[Infiforge — Main Orchestration Service]]
- [[Letease — File Sharing]]
- [[Proxly — Distributed VPN Proxy Service]]
- [[QiHMS — Hospital Management System]]
- [[Ringly — Call Attribution]]
- [[Synch — File Sharing]]
- [[Kilimo — Farm Management System]]

## Related Libraries

- [[Flutter Utils Library]]
- [[Flutter payment library]] (empty - needs documentation)

## Technology Stack

- **Framework:** Flutter 3.4+
- **State Management:** Riverpod with Consumables
- **Platforms:** Android, iOS, Web, Windows, macOS, Linux
- **Storage:** Hive, SharedPreferences, flutter_secure_storage
- **Navigation:** GoRouter
- **HTTP:** infiforge_network

## Key Patterns

- Riverpod with Consumables (NOT Provider or BLoC)
- Singleton services with Provider wrappers
- Pages folder (NOT features folder)
- Direct imports for AuthPage and SetupPage (no wrappers)

## Active Work

- Riverpod with Consumables migration (completed 2026-04-29)
- BLoC removal from QiHMS (completed 2026-04-29)
