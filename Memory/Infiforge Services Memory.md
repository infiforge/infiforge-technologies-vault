---
tags:
  - infiforge
  - services
  - configuration
  - memory
  - reference
created: 2026-04-29
updated: 2026-04-29
---

# Infiforge Services Memory

> Single source of truth for all Infiforge service configurations. Last updated: 2026-04-29.

## Quick Reference

```
infiforge: 8000  | bliss: 8100  | compete: 8200  | farmup: 8300
hail: 8400       | letease: 8500  | proxly: 8600  | qihms: 8700
ringly: 8800      | synch: 8900  | kilimo: 11000
```

## Services by Port

| Port | Service | Type | Database | Certificate |
|------|--------|------|---------|------------|
| 8000 | infiforge | internal | MongoDB | yes |
| 8100 | bliss | internal | MongoDB | yes |
| 8200 | compete | internal | MongoDB | yes |
| 8300 | farmup | internal | MongoDB | yes |
| 8400 | hail | internal | MongoDB | yes |
| 8500 | letease | internal | MongoDB | yes |
| 8600 | proxly | internal | MongoDB | yes |
| 8700 | qihms | internal | MongoDB | yes |
| 8800 | ringly | internal | MongoDB | yes |
| 8900 | synch | internal | MongoDB | yes |
| 11000 | kilimo | external | MySQL | no |

## Critical Paths

### Config Files
- Internal: `/home/dave/work/services/internal/{service}/backend/config.json`
- External: `/home/dave/work/services/external/kilimo/backend/config.json`

### Certificates (MongoDB services)
- `./backend/certs/cloud-db-cert.pem` in each service directory

### Redis (all services)
- Host: 127.0.0.1
- Port: 6379

## Service Discovery

Infiforge monitors all services via ServiceDiscovery. Each config.json MUST have a `default.service` manifest:

```json
"default": {
  "service": {
    "name": "servicename",
    "displayName": "ServiceName",
    "description": "Description",
    "location": "internal" | "external",
    "portRange": { "start": 8000, "end": 8099 },
    "systemd": { "serviceName": "...", "serviceTemplate": "...@{port}.service" },
    "healthEndpoint": "/api/system/health",
    "apiEndpoints": {
      "metrics": "/api/service/metrics",
      "shutdown": "/api/service/shutdown"
    }
  }
}
```

## Health Endpoint

All services expose `/api/system/health`:

```json
{
  "success": true,
  "data": {
    "status": "healthy",
    "service": "servicename",
    "version": "1.0.0",
    "uptime": 3600,
    "modules": {...}
  }
}
```

## MongoDB Credentials

| Service | Database | Username | Password |
|---------|----------|----------|----------|
| bliss | bliss | bliss | TYH5AnHA0BYRT81q |
| compete | compete | compete | qLh3aWXOmEBrOTet |
| farmup | farmup | farmup | CgC9SX6LYWLWPVRC |
| hail | hail | hail | B5ouarOppMh8ld0b |
| infiforge | infiforge | infiforge | bHJ1VX5PfNRMRj3D |
| letease | letease | letease | N5LQ8VeweZQNgfXp |
| proxly | proxly | proxly | 9qcDaCiD2KzXbtWI |
| qihms | qihms | qihms | NItfbIVzPE9Zj34n |
| ringly | ringly | ringly | vAIf7auXvJqjvvxO |
| synch | synch | synch | mkTiwtsz1GOC8JJh |

> Full Atlas URIs are stored in each service's config.json

## MySQL (kilimo)

- Host: localhost
- Port: 3306
- Database: kilimo
- User: kilimo
- Password: kilimo

## Module Order (14 modules)

All services initialize in this exact order:

1. config
2. logger
3. redis
4. network
5. auth
6. static
7. activity
8. ai
9. routes
10. isc
11. setup
12. system-utils
13. observability
14. database

## Cross-Service Monitoring

Infiforge (port 8000) is the monitoring hub:

1. **ServiceDiscovery** scans for `backend/config.json` with `default.service` manifest
2. **StatusPollingService** polls `/api/system/health` every 5 seconds
3. **Redis pub/sub** enables real-time status broadcasts
4. **ISC library** handles inter-service messaging

## Key Files

- Workplan: `/home/dave/work/workplan.md`
- Service configs: See "Critical Paths" above

## Notes

- All 11 services have `default.service` config section
- kilimo uses MySQL, not MongoDB (no cert required)
- All MongoDB services use X.509 cert auth via `./backend/certs/cloud-db-cert.pem`

---

*Memory last updated: 2026-04-29*
*Source: [[workplan]]*