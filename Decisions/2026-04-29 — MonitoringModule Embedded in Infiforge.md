---
date: 2026-04-29
tags:
  - decision
  - architecture
  - monitoring
  - infiforge
---

# 2026-04-29 — MonitoringModule Embedded in Infiforge

## Context

MonitoringModule was initially considered for extraction as a shared library for all services. However, Infiforge's monitoring system has a dual role: it monitors other services AND can be monitored itself.

## Decision

Keep MonitoringModule embedded in Infiforge backend. Do not extract to shared library. Other services communicate with Infiforge via ISC (Inter-Service Communication).

## Rationale

- **Dual Role**: Infiforge is both monitor and monitored
- **Complexity**: Extraction would require major refactoring
- **ISC Pattern**: Services already communicate via Redis pub/sub
- **Simplicity**: Keep monitoring logic centralized in Infiforge

## Implementation

### Infiforge Monitoring System

Infiforge backend contains:
- StatusService - Service status tracking
- StatusPollingService - Periodic status checks
- InstanceMetricsService - Instance metrics collection

### Inter-Service Communication (ISC)

Other services communicate with Infiforge via:
- Redis pub/sub channels
- Status broadcasting
- Config reactivity
- Module status propagation

### Why Not Extract?

1. **Complex Dependencies**: MonitoringModule depends on Infiforge-specific services
2. **Circular Dependency**: Infiforge would need to import its own module
3. **Dual Role**: Monitor vs monitored logic tightly coupled
4. **ISC Already Works**: Services communicate via Redis, no need for shared module

## Alternatives Considered

1. **Extract to @infiforge/monitoring library**
   - Rejected: Would require major refactoring, circular dependencies

2. **Create separate monitoring service**
   - Rejected: Adds complexity, Infiforge already handles this

3. **Use external monitoring (Prometheus, Grafana)**
   - Rejected: Complementary, not replacement for internal monitoring

## Impact

- MonitoringModule remains in Infiforge backend
- Other services use ISC to communicate with Infiforge
- Infiforge acts as central monitoring hub
- Redis enables real-time cross-service status coordination
- Observability library (@infiforge/observability) used for metrics/tracing

## Status

✅ Decision made (2026-04-29)
