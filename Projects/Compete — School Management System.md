---
date: 2026-04-11
tags:
  - project
  - service
  - education
  - school-management
---

# Compete - School & Institution Management System

## AGENTS.md

- **Codebase:** `services/internal/compete/AGENTS.md`
- **Description:** Comprehensive AI agent guide for Compete service

## Service Details

| Attribute | Value |
|-----------|-------|
| **Name** | Compete |
| **Type** | Full-stack application (monorepo) |
| **Location** | `services/internal/compete/` |

## Description

Comprehensive school/institution management system designed for the Kenyan market but extensible globally. Supports institutions from single classroom to multi-campus universities (50,000+ students).

## Architecture

```
compete/
├── frontend/          # Flutter cross-platform app
│   └── lib/          # Dart source code
└── backend/          # Deno API server
    ├── routes/       # API route handlers
    ├── services/     # Business logic
    └── models/       # Data models
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

## Key Features (Core Modules)

1. **Setup & Onboarding**
   - Multi-mode setup (new/existing institution)
   - Device role configuration (server/client)
   - Network discovery (mDNS/Bonjour)
   - Campus layout configuration

2. **Device & Network Management**
   - Local server setup (Deno + MongoDB)
   - Hybrid mode switching
   - QR code connection

3. **Campus Infrastructure**
   - Multi-campus support
   - Building and room management
   - Interactive campus map builder

4. **Academics**
   - Curriculum management
   - Timetabling
   - Attendance tracking
   - Assessment/grading

5. **Finance**
   - Fee structure
   - Mpesa integration (Kenya)
   - Payment tracking

6. **User Management**
   - Role-based access control (RBAC)
   - Bulk import
   - Guardian-student linking

7. **Additional Modules**
   - Transport management
   - Library resources
   - Exams & results
   - Discipline & welfare
   - Hostel management
   - Analytics & dashboards

## Institution Types Supported

- Pre-primary/Kindergarten
- Primary Schools
- Secondary Schools
- Technical/Vocational
- Colleges
- Universities
- Training Centers

## Roles & Permissions

- Super Admin (system-wide)
- Institution Admin
- Managers/Coordinators
- Teachers/Lecturers
- Support Staff
- Transport Staff
- Students/Learners
- Guardians/Parents

## Kenyan Market Defaults

- **Timezone:** Africa/Nairobi
- **Currency:** KES
- **Grading Systems:** KCPE, KCSE, CBC, University GPA

## Status

- ✅ Active development
- ✅ Nx monorepo structure
- ✅ Hono migration complete
- ✅ Riverpod with Consumables migration complete
- ✅ ServiceInstance base class pattern implemented
- ✅ UniversalRoute pattern implemented
- ✅ Port configuration fixed (8200-8299)
- ✅ Tested and working (2026-04-29)

## Notes

- Uses infiforge libraries
- Offline-first Flutter design
- Multi-tenant support (SaaS model)

## Release Information

> [!info] Added: 2026-04-29

### Repository URLs

- GitLab: https://gitlab.com/infiforge1/compete
- GitHub: https://github.com/infiforge/compete

### Local Path
```
~/work/services/internal/compete
```

### Push
```bash
git push all main
```