---
date: 2026-04-29
tags:
  - area
  - infrastructure
  - devops
  - deployment
---

# Infrastructure

## Focus

Infrastructure management for Infiforge services including deployment, monitoring, and CI/CD.

## Related Projects

- [[Infiforge — Main Orchestration Service]] (central monitoring hub)
- [[Infiforge Infrastructure]]

## Related Libraries

- [[System Utils Library]] (service management)
- [[Observability Library]] (OpenTelemetry + Prometheus)

## Key Decisions

- [[2026-04-29 — MonitoringModule Embedded in Infiforge]]

## Infrastructure Components

### Port Ranges

| Service | Port Range |
|---------|------------|
| Infiforge | 8000-8099 |
| Bliss | 8100-8199 |
| Compete | 8200-8299 |
| Farmup | 8300-8399 |
| Hail | 8400-8499 |
| Letease | 8500-8599 |
| Proxly | 8600-8699 |
| Qihms | 8700-8799 |
| Ringly | 8800-8899 |
| Synch | 8900-8999 |
| Kilimo | 11000-11099 |

### Access Methods

- Phone (Tailnet IP)
- Tailnet IP (Tailscale)
- Tailscale Funnel (public)
- Local network

### CI/CD

- GitLab CI for building Flutter apps
- Automatic releases on tag push
- Linux (x64) builds with .tar.gz and .deb packages

### Monitoring

- Infiforge as central monitoring hub
- ISC (Inter-Service Communication) via Redis
- OpenTelemetry for distributed tracing
- Prometheus for metrics

## Active Work

- ServiceInstance refactoring (completed 2026-04-29)
- Port configuration fixes (completed 2026-04-29)
