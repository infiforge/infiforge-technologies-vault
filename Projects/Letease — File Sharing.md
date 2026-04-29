---
date: 2026-04-11
tags:
  - project
  - service
  - file-sharing
  - download-manager
---

# Letease - File Sharing & Download Manager

## Service Details

| Attribute | Value |
|-----------|-------|
| **Name** | Letease |
| **Type** | Full-stack application (Nx monorepo) |
| **Location** | `services/internal/letease/` |
| **Port Range** | 8500-8599 |

## Description

File sharing application, download manager, proxy client, torrent downloader, and link generator. Allows users to move files to personal online storage when networks block protocols.

**Note:** Description appears similar to Farmup - may need verification if this is duplicate or separate service.

## Architecture

```
letease/
├── frontend/          # Flutter cross-platform app
├── backend/           # Node.js API server
│   ├── server.js      # Main server
│   ├── routes/        # API routes
│   └── models/        # Database models
└── extension/         # Browser extension
```

## Technology Stack

### Backend
- **Runtime:** Deno (TypeScript)
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
- Proxy client (HTTP/HTTPS/SOCKS)
- Torrent downloader
- Link generator with QR codes
- Browser extension

## Status

- Active service
- Requires migration to Deno + Hono
- Requires migration to Riverpod with Consumables

## Notes

- Uses infiforge libraries
- Similar to Farmup - verify if duplicate