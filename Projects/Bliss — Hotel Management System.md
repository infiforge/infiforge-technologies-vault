---
date: 2026-04-11
tags:
  - project
  - service
  - hotel-management
---

# Bliss - Hotel Management System (HMS)

## AGENTS.md

- **Codebase:** `services/internal/bliss/AGENTS.md`
- **Description:** Comprehensive AI agent guide for Bliss service

## Service Details

| Attribute | Value |
|-----------|-------|
| **Name** | Bliss |
| **Type** | Full-stack application |
| **Location** | `services/internal/bliss/` |
| **Port Range** | 8100-8199 |

## Description

Comprehensive Hotel Management System for streamlining hotel operations, guest experiences, and improving overall efficiency. Cross-platform solution for desktop, web, and mobile.

## Architecture

```
bliss/
├── frontend/         # Flutter cross-platform app
│   ├── lib/          # Dart source code
│   ├── pubspec.yaml  # Flutter dependencies
│   └── platforms: Android, iOS, Web, Windows, macOS, Linux
├── backend/          # Deno API server
│   ├── server.ts     # Main server entry point
│   ├── routes/       # API route handlers
│   ├── services/     # Business logic services
│   └── models/       # Data models
└── extension/        # Browser extension (if applicable)
```

## Technology Stack

### Backend
- **Runtime:** Deno (TypeScript)
- **HTTP Framework:** Hono ✅
- **Database:** MongoDB
- **Real-time:** WebSockets
- **Auth:** JWT with OAuth (Google, Microsoft, Apple)
- **Architecture:** ServiceInstance base class pattern ✅
- **Routes:** UniversalRoute pattern ✅

### Frontend
- **Framework:** Flutter
- **State Management:** Riverpod with Consumables ✅
- **Platforms:** Android, iOS, Web, Windows, macOS, Linux

## Key Features

- User management with role-based access control
- Activity tracking for audit trails
- Room booking and reservation management
- Guest check-in/check-out workflows
- Room availability and status tracking
- Invoicing and billing generation
- Payment tracking
- Financial reporting
- Integrated setup wizard
- Multi-property support

## Code Conventions

### Backend (Deno)
- Use TypeScript with strict mode
- Follow RESTful API design patterns
- Use async/await for asynchronous operations
- Include JSDoc comments for public APIs

### Frontend (Flutter)
- Use Riverpod with Consumables (NOT Provider or Bloc)
- Follow Flutter's declarative UI pattern
- Prefer StatelessWidget when no state needed

## Development Commands

```bash
# Navigate to service
cd services/internal/bliss

# Backend development
nx run backend:serve        # Development with hot reload

# Frontend development  
nx run frontend:serve       # Development server

# Full stack
nx run serve               # Start both frontend and backend
```

## Security

- Never log sensitive guest data (credit cards, personal info)
- JWT tokens must have expiration
- Implement refresh token rotation
- Store tokens securely on device

## Status

- ✅ Active service
- ✅ Nx monorepo structure
- ✅ Hono migration complete
- ✅ Riverpod with Consumables migration complete
- ✅ ServiceInstance base class pattern implemented
- ✅ UniversalRoute pattern implemented
- ✅ Port configuration fixed (8100-8199)
- ✅ Tested and working (2026-04-29)

## Notes

- Uses infiforge libraries
- Config via config.json (not .env)
- Service-specific setup required

## Release Information

> [!info] Added: 2026-04-29

### Repository URLs

| Service | GitLab | GitHub |
|---------|-------|-------|
| **Bliss** | https://gitlab.com/infiforge1/bliss | https://github.com/infiforge/bliss |

### Git Remotes

| Remote | URL | Purpose |
|--------|-----|---------|
| `origin` | git@gitlab.com:infiforge1/bliss.git | Primary (GitLab) |
| `github` | git@github.com:infiforge/bliss.git | Secondary |
| `all` | git@gitlab.com + git@github.com | Push to both |

### Local Path
```
~/work/services/internal/bliss
```

### Push Commands
```bash
git push all main
git tag flutter-v1.0.0
git push all flutter-v1.0.0
```