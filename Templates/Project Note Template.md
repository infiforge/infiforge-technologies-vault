---
date: 2026-04-29
tags:
  - template
  - project
  - service
---

# Project Note Template

Use this template for new service/project notes.

## Frontmatter

```yaml
---
date: YYYY-MM-DD
tags:
  - project
  - service
  - [category]
---
```

## Content Template

```markdown
# [Service Name] — [Type]

## Service Details

| Attribute | Value |
|-----------|-------|
| **Name** | [Service Name] |
| **Type** | Full-stack application (Nx monorepo) |
| **Location** | `services/internal/[service-name]/` |
| **Port Range** | XXXX-XXXXX |

## Description

[Brief description of what the service does]

## Architecture

```
[Folder structure diagram]
```

## Technology Stack

### Backend
- **Runtime:** Deno (TypeScript)
- **HTTP Framework:** Hono ✅
- **Database:** MongoDB
- **Architecture:** ServiceInstance base class pattern ✅
- **Routes:** UniversalRoute pattern ✅

### Frontend
- **Framework:** Flutter
- **State Management:** Riverpod with Consumables ✅
- **Platforms:** Android, iOS, Web, Desktop

## Key Features

- [Feature 1]
- [Feature 2]
- [Feature 3]

## Development Commands

```bash
cd services/internal/[service-name]

# Backend
nx run backend:serve

# Frontend
nx run frontend:serve

# Full stack
nx run serve
```

## Status

- ✅ Active service
- ✅ ServiceInstance base class pattern implemented
- ✅ UniversalRoute pattern implemented
- ✅ Port configuration fixed (XXXX-XXXXX)
- ✅ Tested and working (YYYY-MM-DD)

## Release Information

### Repository URLs

| Service | GitLab | GitHub |
|---------|-------|-------|
| **[Service Name]** | https://gitlab.com/infiforge1/[service] | https://github.com/infiforge/[service] |

### Local Path
```
~/work/services/internal/[service-name]
```

### Push Commands
```bash
git push all main
```
```
