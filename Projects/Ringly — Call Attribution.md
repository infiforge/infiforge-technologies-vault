---
date: 2026-04-11
tags:
  - project
  - service
  - marketing
  - call-tracking
---

# Ringly - Call Attribution System

## Service Details

| Attribute | Value |
|-----------|-------|
| **Name** | Ringly (also known as CallAttribution) |
| **Type** | Full-stack application (Nx monorepo) |
| **Location** | `services/internal/ringly/` |
| **Port Range** | 8010-8099 |

## Description

Call tracking and attribution system for Google Ads campaigns with offline conversion tracking. Self-hosted solution for Kenyan and African markets. Tracks offline conversions from phone calls by attributing them to specific ad campaigns.

## Architecture

```
ringly/
├── backend/          # Deno API server
│   ├── server.ts     # Main server
│   ├── routes/       # API routes
│   └── services/     # Business logic
├── frontend/         # Flutter cross-platform app
│   └── lib/          # Dart source code
├── tracker/          # Phone call tracking component
└── docker/           # Docker deployment
```

## Technology Stack

### Backend
- **Runtime:** Deno (TypeScript)
- **Web Framework:** Oak or Hono (should be Hono)
- **Database:** MongoDB
- **Auth:** JWT
- **External APIs:** Google Ads API (offline conversions)

### Frontend
- **Framework:** Flutter
- **State Management:** Provider (should be Riverpod with Consumables)
- **Charts:** fl_chart

## Key Features

### GCLID Tracking
- Capture Google Click ID from ad clicks
- Store GCLID with phone number mappings
- Attribution window (30-90 days)

### Dynamic Number Insertion (DNI)
- Replace phone numbers on client websites
- Different numbers per campaign/source
- Session-based number assignment

### Offline Conversion Tracking
- Send conversions to Google Ads API
- Conversion value and currency
- Scheduled uploads (hourly/daily)

### Additional Features
- DTMF/IVR integration
- SMS/WhatsApp notifications
- Multi-tenant for agencies
- Call analytics dashboard

## African Market Considerations

- **Phone format:** +254 (Kenya)
- **Timezone:** Africa/Nairobi (EAT)
- **SMS gateways:** Twilio, Africa's Talking
- **Regulations:** Kenya Data Protection Act

## Status

- Active service
- Requires migration to Hono
- Requires migration to Riverpod with Consumables

## Notes

- Uses infiforge Deno libraries
- Google Ads API integration critical
- Multi-tenant for agencies and clients

## Release Information

> [!info] Added: 2026-04-29

- GitLab: https://gitlab.com/infiforge1/ringly
- GitHub: https://github.com/infiforge/ringly
- Path: `~/work/services/internal/ringly`
- Push: `git push all main`