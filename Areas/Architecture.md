---
date: 2026-04-29
tags:
  - area
  - architecture
  - design
  - patterns
---

# Architecture

## Focus

Architectural decisions and patterns across Infiforge services.

## Related Projects

All 11 services follow the same architecture:
- [[Bliss — Hotel Management System]]
- [[Compete — School Management System]]
- [[Farmup — Farm Management System]]
- [[Hail — Skill Sharing Marketplace]]
- [[Infiforge — Main Orchestration Service]]
- [[Letease — File Sharing]]
- [[Proxly — Distributed VPN Proxy Service]]
- [[QiHMS — Hospital Management System]]
- [[Ringly — Call Attribution]]
- [[Synch — File Sharing]]
- [[Kilimo — Farm Management System]]

## Key Decisions

- [[2026-04-29 — ServiceInstance Base Class Pattern]]
- [[2026-04-28 — UniversalRoute Pattern]]
- [[2026-04-29 — Config-First Architecture]]
- [[2026-04-29 — MonitoringModule Embedded in Infiforge]]

## Architectural Patterns

### ServiceInstance Pattern

All services extend ServiceInstance base class with canonical lifecycle:
- initialize() → configure() → start() → stop() → restart()
- 14 modules in canonical order
- Config-driven architecture

### UniversalRoute Pattern

Single route definition accessible via HTTP, WebSocket, and GraphQL:
- Shared interfaces from @infiforge/routes
- graphqlTypeDefs required for each route
- Standardized error handling

### Config-First Architecture

- config.json as single source of truth
- No .env files
- Config library handles all configuration
- Runtime reconfiguration support

### Library Module Pattern

All library modules implement:
- initialize()
- configure(instance, options)
- start(instance?)
- stop()
- restart()

## Active Work

- ServiceInstance refactoring (completed 2026-04-29)
- UniversalRoute pattern implementation (completed 2026-04-28)
