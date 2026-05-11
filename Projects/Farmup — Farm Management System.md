---
date: 2026-04-11
tags:
  - project
  - service
  - agriculture
  - farm-management
---

# Farmup - Farm Management System

## AGENTS.md

- **Codebase:** `services/internal/farmup/AGENTS.md`
- **Description:** Comprehensive AI agent guide for Farmup service

## Service Details

| Attribute | Value |
|-----------|-------|
| **Name** | Farmup |
| **Type** | Full-stack application (Nx monorepo) |
| **Location** | `services/internal/farmup/` |
| **Port Range** | 8300-8399 |

## Description

Comprehensive farm/agriculture management system. Cross-platform solution for desktop, web, and mobile with browser extension.

## Architecture

```
farmup/
├── frontend/          # Flutter cross-platform app
│   └── lib/           # Dart source code
├── backend/           # Node.js/Deno API server
│   ├── server.ts      # Main server
│   ├── routes/        # API routes
│   ├── services/      # Business logic
│   └── models/        # Data models
└── extension/         # Browser extension
```

## Technology Stack

### Backend
- **Runtime:** Deno (TypeScript)
- **Web Framework:** Hono ✅
- **API:** GraphQL (Apollo Server)
- **Database:** MongoDB (Mongoose)
- **Cache:** Redis
- **Real-time:** Socket.IO, GraphQL-WS
- **Architecture:** ServiceInstance base class pattern ✅
- **Routes:** UniversalRoute pattern ✅

### Frontend
- **Framework:** Flutter
- **State Management:** Riverpod with Consumables ✅
- **Storage:** Hive
- **Platforms:** Android, iOS, Web, Desktop

## Key Features

- Crop management
- Livestock management
- Field/farm plotting
- Harvest tracking
- Equipment management
- Financial tracking for farm operations
- Weather integration
- Task scheduling
- Report generation

## Development Commands

```bash
cd services/internal/farmup

# Backend
nx run backend:serve
nx run backend:build

# Frontend
nx run frontend:serve
nx run frontend:build

# Full stack
nx run serve
```

## Status

- ✅ Active service
- ✅ Nx monorepo structure
- ✅ Deno + Hono migration complete
- ✅ Riverpod with Consumables migration complete
- ✅ ServiceInstance base class pattern implemented
- ✅ UniversalRoute pattern implemented
- ✅ Port configuration fixed (8300-8399)
- ✅ Tested and working (2026-04-29)

## Notes

- Uses infiforge libraries
- Config via config.json (not .env)
- Browser extension for quick access

## Release Information

> [!info] Added: 2026-04-29

- GitLab: https://gitlab.com/infiforge1/farmup
- GitHub: https://github.com/infiforge/farmup
- Path: `~/work/services/internal/farmup`
- Push: `git push all main`