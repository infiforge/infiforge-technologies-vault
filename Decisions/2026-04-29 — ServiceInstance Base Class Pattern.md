---
date: 2026-04-29
tags:
  - decision
  - architecture
  - service-instance
  - lifecycle
---

# 2026-04-29 — ServiceInstance Base Class Pattern

## Context

All 11 Infiforge services needed a unified architecture pattern to ensure consistency across the codebase. Previously, services had varying initialization patterns, making maintenance difficult and error-prone.

## Decision

Implemented a ServiceInstance base class that all services extend, providing a canonical lifecycle pattern.

## Rationale

- **Consistency**: All services follow the same initialization, configuration, start, stop, and restart pattern
- **Maintainability**: Changes to lifecycle logic only need to be made in one place
- **Predictability**: Developers know exactly what to expect when working with any service
- **Testability**: Standardized lifecycle makes testing easier

## Implementation

### Canonical Module Order (14 modules)

All services initialize, configure, and start modules in this exact order:

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

### Lifecycle Methods

Each service must implement:
- `initialize()` - Load and configure all modules
- `configure()` - Re-configure modules with latest config
- `start()` - Start network, register routes, start all modules
- `stop()` - Stop all modules in reverse order
- `restart()` - Stop → configure → start
- `static launch()` - Static entry point for service startup

### Module Contract

Every library module implements:
- `initialize()` - Create singleton, idempotent
- `configure(instance, options)` - Store options for later use
- `start(instance?)` - Register routes if applicable
- `stop()` - Clean up resources
- `restart()` - stop() → configure() → start()

## Alternatives Considered

1. **No base class** - Each service implements its own lifecycle
   - Rejected: Too much duplication, inconsistent patterns

2. **Abstract class with required methods** - Force implementation
   - Rejected: Too rigid, some services need flexibility (e.g., Infiforge)

3. **Mixin pattern** - Compose lifecycle from mixins
   - Rejected: More complex, harder to understand

## Impact

- All 11 services now extend ServiceInstance
- Infiforge uses specialized pattern (not ServiceInstance) due to monitoring role
- All services use same 14 library modules
- Config-driven architecture (no .env files)
- Reactive behavior for status/config/lifecycle propagation

## Status

✅ Implemented and tested (2026-04-29)
