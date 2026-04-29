---
date: 2026-04-11
tags:
  - project
  - service
  - file-sharing
  - download-manager
---

# Synch - File Sharing Application

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
- **Runtime:** Deno (should be - may need migration)
- **Web Framework:** Hono (should be - may need migration)
- **Database:** MongoDB
- **Auth:** JWT

### Frontend
- **Framework:** Flutter
- **State Management:** Provider (should be Riverpod with Consumables)
- **Storage:** Hive

## Key Features

- File sharing and uploads
- Download manager with pause/resume
- Proxy client (HTTP/SOCKS)
- Torrent downloader
- Link generator with QR codes

## Status

- Active service
- Requires migration to Deno + Hono
- Requires migration to Riverpod with Consumables
- Note: Similar to Letease and Farmup - verify if duplicate

## Notes

- Uses infiforge libraries
- Config via config.json