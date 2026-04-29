---
date: 2026-04-29
updated: 2026-04-29
tags:
  - library
  - deno
  - isc
  - inter-service-communication
---

# ISC Library

## Overview

ISC (Inter-Service Communication) library enables real-time communication between Infiforge services via Redis pub/sub. Services use ISC to broadcast status, coordinate configuration changes, and share events.

## Purpose

- Enable real-time cross-service communication
- Support status broadcasting and monitoring
- Enable configuration reactivity across services
- Provide event-driven architecture

## Key Features

- Redis pub/sub for real-time messaging
- Service status broadcasting
- Configuration change propagation
- Event subscription and publishing
- Channel-based communication

## Module Pattern

```typescript
initialize(): Promise<void>
configure(instance: ServiceInstance, options: ISCOptions): Promise<void>
start(instance?: ServiceInstance): Promise<void>
stop(): Promise<void>
restart(): Promise<void>
```

## Usage

```typescript
import { ISCModule } from "@infiforge/isc";

// In service initialize()
this.iscModule = new ISCModule();
await this.iscModule.initialize();
await this.iscModule.configure(this, {
  redis: this.config.get("redis"),
  channels: {
    status: "infiforge:status",
    config: "infiforge:config",
    events: "infiforge:events"
  }
});

// Broadcast status
await this.iscModule.publish("status", {
  service: "bliss",
  status: "running",
  port: 8100
});

// Subscribe to events
await this.iscModule.subscribe("config", (message) => {
  console.log("Config changed:", message);
});
```

## Configuration Options

```json
{
  "isc": {
    "enabled": true,
    "redis": {
      "host": "localhost",
      "port": 6379
    },
    "channels": {
      "status": "infiforge:status",
      "config": "infiforge:config",
      "events": "infiforge:events"
    }
  }
}
```

## Dependencies

- Redis connection (via @infiforge/redis)
- Config library

## Services Using It

All services use ISC for cross-service communication:
- Bliss, Compete, Farmup, Hail, Letease, Proxly, Qihms, Ringly, Synch, Kilimo
- Infiforge uses ISC as central monitoring hub

## Location

`/home/dave/work/libraries/deno/isc/`
