---
date: 2026-04-29
updated: 2026-04-29
tags:
  - library
  - deno
  - base
  - service-instance
---

# Base Library

## Overview

Base library provides the ServiceInstance base class that all Infiforge services extend. This is the foundation of the canonical lifecycle pattern.

## Purpose

- Define ServiceInstance base class with lifecycle methods
- Provide canonical module initialization order
- Enable consistent service architecture across all services
- Support reactive status and configuration propagation

## Key Features

- ServiceInstance base class with lifecycle methods
- Canonical module order (14 modules)
- Reactive status tracking
- Configuration reactivity
- Module lifecycle management

## Module Pattern

All library modules follow this pattern:

```typescript
initialize(): Promise<void>
// - No parameters
// - Creates singleton service if not exists
// - Idempotent (safe to call multiple times)

configure(instance: ServiceInstance, options: ModuleOptions): Promise<void>
// - First param: service instance (for accessing logger, config, etc.)
// - Second param: module-specific options from config.json
// - Stores options for later use

start(instance?: ServiceInstance): Promise<void>
// - Optional instance parameter (needed for modules that register routes)
// - Registers routes on Hono app if applicable
// - Marks service as running

stop(): Promise<void>
// - Cleans up resources
// - Marks service as stopped

restart(): Promise<void>
// - Strict order: stop() -> configure() -> start()
```

## Canonical Module Order

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

## Usage

```typescript
import { ServiceInstance } from "@infiforge/base";

export class MyService extends ServiceInstance {
  async initialize(): Promise<void> {
    // Initialize modules in canonical order
    await this.configModule.initialize();
    await this.loggerModule.initialize();
    // ... etc
  }

  async configure(): Promise<void> {
    // Re-configure all modules
    await this.configModule.configure(this, this.config.get("config"));
    await this.loggerModule.configure(this, this.config.get("logger"));
    // ... etc
  }

  async start(): Promise<void> {
    // Start network and register routes
    await this.networkModule.start(this);
    await this.routesModule.start(this);
    // ... etc
  }

  async stop(): Promise<void> {
    // Stop modules in reverse order
    await this.databaseModule.stop();
    await this.observabilityModule.stop();
    // ... etc
  }

  static async launch(port?: number): Promise<MyService> {
    const service = new MyService();
    await service.initialize();
    await service.configure();
    await service.start();
    return service;
  }
}
```

## Dependencies

- No external dependencies
- Deno standard library only

## Services Using It

All 11 services extend ServiceInstance:
- Bliss, Compete, Farmup, Hail, Infiforge (special case), Letease, Proxly, Qihms, Ringly, Synch, Kilimo

## Location

`/home/dave/work/libraries/deno/base/`
