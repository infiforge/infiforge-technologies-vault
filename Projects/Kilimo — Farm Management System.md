---
date: 2026-04-29
tags:
  - project
  - service
  - agriculture
  - external
---

# Kilimo - Farm Management System

## Service Details

| Attribute | Value |
|-----------|-------|
| **Name** | Kilimo |
| **Type** | Full-stack application |
| **Location** | `services/external/kilimo/` |
| **Port Range** | 11000-11099 |
| **External** | Yes |

## Description

Farm input management system for organizations to manage their farmers. A comprehensive farming solution for Kenyan and African farmers to optimize planting decisions, manage farms, and track records.

## Architecture

```
kilimo/
├── frontend/         # Flutter cross-platform app
│   ├── lib/          # Dart source code
│   ├── pubspec.yaml  # Flutter dependencies
│   └── platforms: Android, iOS, Web, Windows, macOS, Linux
├── backend/          # Deno API server
│   ├── server.ts     # Main server entry point
│   ├── routes/       # API route handlers
│   ├── services/     # Business logic services
│   └── models/       # Data models
```

## Technology Stack

### Backend
- **Runtime:** Deno (TypeScript)
- **HTTP Framework:** Hono
- **Database:** MongoDB
- **Real-time:** WebSockets

### Frontend
- **Framework:** Flutter

## Release Information

> [!info] Added: 2026-04-29

### Repository URLs

| Service | GitLab | GitHub |
|---------|-------|-------|
| **Kilimo** | https://gitlab.com/infiforge1/kilimo | https://github.com/infiforge/kilimo |

### Git Remotes

| Remote | URL | Purpose |
|--------|-----|---------|
| `origin` | git@gitlab.com:infiforge1/kilimo.git | Primary (GitLab) |
| `github` | git@github.com:infiforge/kilimo.git | Secondary |
| `all` | git@gitlab.com + git@github.com | Push to both |

### Local Path
```
~/work/services/external/kilimo
```

### Push Commands
```bash
# Push to both GitLab AND GitHub
git add .
git commit -m "Update"
git push all main

# Create release tag
git tag flutter-v1.0.0
git push all flutter-v1.0.0
```

### CI/CD Pipeline

Each service has `.gitlab-ci.yml` that:
1. Builds Flutter app for Linux (x64)
2. Creates `.tar.gz` archive
3. Creates `.deb` package
4. On tag push: creates GitLab release

### Related Services
- [[Farmup — Farm Management System]] (internal equivalent)