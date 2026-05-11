---
date: 2026-04-11
tags:
  - project
  - service
  - file-sharing
  - download-manager
---

# Synch - File Sharing Application

## AGENTS.md

- **Codebase:** `services/internal/synch/AGENTS.md`
- **Description:** Comprehensive AI agent guide for Synch service

## Service Details

| Attribute | Value |
|-----------|-------|
| **Name** | Synch |
| **Type** | Full-stack application (Nx monorepo) |
| **Location** | `services/internal/synch/` |
| **Port Range** | 8800-8899 |

## Description

File sharing application, download manager, proxy client, torrent downloader, and link generator. Similar functionality to Letease and Farmup - may be duplicate or specialized version.

## Architecture

```
synch/
├── backend/          # Node.js API server
│   ├── server.ts     # Main server
│   ├── routes/       # API routes
│   └── models/       # Database models
└── frontend/         # Flutter cross-platform app
    └── lib/          # Dart source code
```

## Technology Stack

### Backend
- **Runtime:** Deno (TypeScript)
- **Web Framework:** Hono ✅
- **Database:** MongoDB
- **Auth:** JWT
- **Architecture:** ServiceInstance base class pattern ✅
- **Routes:** UniversalRoute pattern ✅

### Frontend
- **Framework:** Flutter
- **State Management:** Riverpod with Consumables ✅
- **Storage:** Hive

## Key Features

- File sharing and uploads
- Download manager with pause/resume
- Proxy client (HTTP/SOCKS)
- Torrent downloader
- Link generator with QR codes

## Status

- ✅ Active service
- ✅ Deno + Hono migration complete
- ✅ Riverpod with Consumables migration complete
- ✅ ServiceInstance base class pattern implemented
- ✅ UniversalRoute pattern implemented
- ✅ Port configuration fixed (8900-8999)
- ✅ Tested and working (2026-04-29)

## Notes

- Uses infiforge libraries
- Config via config.json

## Release Information

> [!info] Added: 2026-04-29

- GitLab: https://gitlab.com/infiforge1/synch
- GitHub: https://github.com/infiforge/synch
- Path: `~/work/services/internal/synch`
- Push: `git push all main`