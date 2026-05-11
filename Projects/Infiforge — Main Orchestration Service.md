---
date: 2026-04-11
tags:
  - project
  - service
  - orchestration
  - main-service
---

# Infiforge - Main Orchestration Service

## AGENTS.md

- **Codebase:** `services/internal/infiforge/AGENTS.md`
- **Description:** Comprehensive AI agent guide for Infiforge service

## Service Details

| Attribute | Value |
|-----------|-------|
| **Name** | Infiforge |
| **Type** | Full-stack application (Nx monorepo) |
| **Location** | `services/internal/infiforge/` |
| **Port Range** | 8000-8099 |

## Description

Innovative Software Solutions platform - Main orchestration service. This is the central service that coordinates all other Infiforge services.

## Architecture

```
infiforge/
├── backend/          # Deno API server
│   ├── server.ts     # Main server
│   ├── routes/       # API route handlers
│   ├── services/     # Business logic
│   ├── interfaces/   # TypeScript interfaces
│   └── config.json   # Configuration
└── frontend/         # Flutter cross-platform app
    ├── lib/          # Dart source code
    └── pubspec.yaml  # Dependencies
```

## Technology Stack

### Backend (GOOD - follows standards!)
- **Runtime:** Deno (TypeScript with strict mode)
- **HTTP Framework:** Hono ✓ (correct!)
- **Database:** MongoDB (cloud cluster with X509 certificate auth)
- **Cache:** Redis (sessions, real-time data)
- **API:** GraphQL (via graphql-yoga)
- **Auth:** JWT with Argon2 password hashing

### Frontend
- **Framework:** Flutter 3.4+
- **State Management:** Riverpod with Consumables ✅
- **Storage:** Hive
- **Platforms:** Android, iOS, Web, Desktop

## Database Connection

- MongoDB: Cloud cluster with X509 certificate auth
- Certificate: `certs/cloud-db-cert.pem`
- Auto-reconnection with exponential backoff

## Environment Profiles

| Profile | MongoDB | Logging | Port |
|---------|---------|---------|------|
| default | Cloud | debug | 8000 |
| local | Local | debug | 8000 |
| production | Cloud | error only | 8080 |

## Key Features

- Service orchestration
- Cross-service communication
- User management
- System configuration
- Authentication/Authorization

## Development Commands

```bash
cd services/internal/infiforge

# Backend
nx run backend:serve
nx run backend:build
nx run backend:lint

# Frontend
nx run frontend:serve
nx run frontend:build

# Full stack
nx run serve
```

## Status

- ✅ Uses Deno + Hono
- ✅ Uses GraphQL with graphql-yoga
- ✅ Uses Argon2 for password hashing
- ✅ Uses Redis for sessions
- ✅ Riverpod with Consumables migration complete
- ✅ Port configuration fixed (8000-8099)
- ✅ Tested and working (2026-04-29)
- Note: Special case - custom architecture preserved (not ServiceInstance pattern)

## Notes

- Main orchestration service for all Infiforge services
- Uses infiforge Deno libraries
- Config via config.json
- Frontend needs migration to Riverpod with Consumables

## Release Information

> [!info] Added: 2026-04-29

- GitLab: https://gitlab.com/infiforge1/infiforge
- GitHub: https://github.com/infiforge/infiforge
- Path: `~/work/services/internal/infiforge`
- Push: `git push all main`