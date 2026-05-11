---
date: 2026-04-11
tags:
  - project
  - service
  - marketplace
  - skill-sharing
---

# Hail - Skill-Sharing Marketplace

## AGENTS.md

- **Codebase:** `services/internal/hail/AGENTS.md`
- **Description:** Comprehensive AI agent guide for Hail service

## Service Details

| Attribute | Value |
|-----------|-------|
| **Name** | Hail |
| **Type** | Frontend-focused (Nx monorepo) |
| **Location** | `services/internal/hail/` |
| **Port Range** | 8400-8499 |

## Description

Cross-platform skill-sharing app similar to Upwork or TaskRabbit. Users can offer skills as services and find work from others seeking specific skillsets.

## Architecture

```
hail/
├── apps/
│   └── frontend/     # Flutter cross-platform app
│       └── lib/      # Dart source code
│           ├── features/    # Feature-based organization
│           ├── services/   # Singleton services
│           └── providers/  # Riverpod providers
└── firebase.json    # Firebase configuration
```

## Technology Stack

### Backend (DIFFERENT - uses Firebase)
- **Platform:** Firebase (Google Cloud)
- **Auth:** Firebase Auth
- **Database:** Firestore (NoSQL)
- **Storage:** Firebase Storage
- **Functions:** Firebase Cloud Functions
- **Notifications:** Firebase Cloud Messaging

### Frontend
- **Framework:** Flutter
- **State Management:** Riverpod + Singleton services
- **Navigation:** GoRouter
- **Platforms:** Android, iOS, Web, Desktop

## Key Features

- **Service Listings** - Users create skill/service listings with categories
- **Task Matching** - Job posting, proposals, matching algorithm
- **In-App Messaging** - Real-time chat between users
- **User Profiles & Ratings** - Portfolio, endorsements, ratings
- **Real-time Notifications** - Push notifications for matches, messages

## Firestore Collections

- users/ - User profiles
- services/ - Service listings
- jobs/ - Job postings
- messages/ - Chat messages
- reviews/ - Ratings and reviews
- categories/ - Skill categories

## Development Commands

```bash
cd services/internal/hail

# Frontend
nx run frontend:serve
flutter run

# Build
nx run frontend:build
flutter build [platform]

# Firebase
firebase emulators:start
firebase deploy
```

## Status

- ✅ Active service
- ✅ Nx monorepo with Firebase backend
- ✅ Uses Riverpod with Consumables
- ✅ ServiceInstance base class pattern implemented
- ✅ Port configuration fixed (8400-8499)
- ✅ Tested and working (2026-04-29)
- Note: Different architecture - uses Firebase instead of Deno backend

## Notes

- Uses Firebase instead of infiforge Deno libraries
- Config via Firebase Console
- Different architecture pattern from other services

## Release Information

> [!info] Added: 2026-04-29

- GitLab: https://gitlab.com/infiforge1/hail
- GitHub: https://github.com/infiforge/hail
- Path: `~/work/services/internal/hail`
- Push: `git push all main`