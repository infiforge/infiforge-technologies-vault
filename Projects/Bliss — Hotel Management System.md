---
date: 2026-04-11
tags:
  - project
  - service
  - hotel-management
---

# Bliss - Hotel Management System (HMS)

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
- **HTTP Framework:** Hono (should be - AGENTS.md says Express/Oak)
- **Database:** MongoDB
- **Real-time:** WebSockets
- **Auth:** JWT with OAuth (Google, Microsoft, Apple)

### Frontend
- **Framework:** Flutter
- **State Management:** Provider / Riverpod (should be Riverpod with Consumables)
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

- Active service
- Nx monorepo structure
- Requires migration to Hono (from Express/Oak)
- Requires migration to Riverpod with Consumables

## Notes

- Uses infiforge libraries
- Config via config.json (not .env)
- Service-specific setup required