---
date: 2026-04-11
tags:
  - project
  - service
  - healthcare
  - hospital-management
---

# QiHMS - Hospital Management System

## Service Details

| Attribute | Value |
|-----------|-------|
| **Name** | QiHMS (Qi Hospital Management System) |
| **Type** | Full-stack healthcare application (Nx monorepo) |
| **Location** | `services/internal/qihms/` |
| **Port Range** | 8700-8799 |

## Description

Comprehensive healthcare platform for streamlining hospital operations and improving patient care. Unified solution for patient records, appointments, billing, pharmacy, laboratory, and ward operations.

## Architecture

```
qihms/
├── backend/          # Deno API server
│   ├── server.ts     # Main server
│   ├── routes/       # API routes
│   ├── services/     # Business logic
│   └── interfaces/   # TypeScript interfaces
└── frontend/         # Flutter cross-platform app
    ├── lib/          # Dart source code
    └── pubspec.yaml  # Dependencies
```

## Technology Stack

### Backend
- **Runtime:** Deno (TypeScript with strict mode)
- **API:** GraphQL with WebSocket support
- **Database:** MongoDB
- **Auth:** OAuth 2.0, JWT
- **Real-time:** WebSocket subscriptions

### Frontend
- **Framework:** Flutter
- **State Management:** Riverpod + BLoC (Note: BLoC should be removed, use only Riverpod with Consumables)
- **Storage:** Hive
- **Platforms:** Web, iOS, Android, Desktop

## Key Features

### Core Modules
- Patient Management
- Electronic Health Records (EHR)
- Appointment Scheduling
- Ward Management (bed allocation, transfers)
- Pharmacy Management
- Laboratory & Radiology
- Billing & Insurance
- Analytics & Reporting

### Additional Features
- Medical history timeline
- Lab results integration
- Drug interaction alerts
- Real-time ward occupancy
- Dashboard with key metrics

## Healthcare Roles

- **Doctors/Physicians** - Full patient access, prescriptions
- **Nurses** - Patient care records, vitals, medications
- **Pharmacists** - Prescription management, inventory
- **Lab Technicians** - Test orders and results
- **Admin Staff** - Scheduling, billing
- **Patients** - Own records only

## Security & Compliance

### HIPAA/GDPR Considerations
- Patient data encrypted at rest
- Access logging (who viewed what record when)
- No PHI in logs
- Consent management
- Data retention policies
- Right to deletion

### Security Checklist
- [x] Encryption at rest and in transit
- [x] Comprehensive audit logging
- [x] Role-based access control
- [ ] Multi-factor authentication (recommended)
- [ ] Session timeout

## Status

- Active service
- Uses Deno backend (good!)
- Uses GraphQL with WebSocket
- Frontend uses Riverpod + BLoC (should remove BLoC, use only Riverpod with Consumables)

## Notes

- Uses infiforge Deno libraries
- Config via config.json
- Healthcare data privacy critical
- Audit logging required for all patient access