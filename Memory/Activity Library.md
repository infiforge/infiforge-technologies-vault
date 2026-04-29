---
date: 2026-04-29
updated: 2026-04-29
tags:
  - library
  - deno
  - activity
  - tracking
---

# Activity Library

## Overview

Activity library provides activity tracking and audit logging for Infiforge services. Tracks user actions, system events, and changes for compliance and debugging.

## Purpose

- Track user activities and actions
- Provide audit logs for compliance
- Enable debugging and troubleshooting
- Support activity history and reporting
- Enable real-time activity monitoring

## Key Features

- Activity logging with timestamps
- User action tracking
- System event logging
- Activity history queries
- Real-time activity streaming
- Compliance-ready audit trails

## Module Pattern

```typescript
initialize(): Promise<void>
configure(instance: ServiceInstance, options: ActivityOptions): Promise<void>
start(instance?: ServiceInstance): Promise<void>
stop(): Promise<void>
restart(): Promise<void>
```

## Usage

```typescript
import { ActivityModule } from "@infiforge/activity";

// Log user action
await this.activityModule.log({
  userId: "user123",
  action: "login",
  resource: "/api/auth/login",
  metadata: { ip: "192.168.1.1" }
});

// Log system event
await this.activityModule.log({
  service: "bliss",
  action: "config_change",
  resource: "config.json",
  metadata: { changedKeys: ["network.http.port"] }
});

// Query activity history
const activities = await this.activityModule.query({
  userId: "user123",
  startDate: new Date("2026-04-01"),
  endDate: new Date("2026-04-30")
});

// Stream real-time activities
this.activityModule.stream((activity) => {
  console.log("New activity:", activity);
});
```

## Configuration Options

```json
{
  "activity": {
    "enabled": true,
    "storage": "database",
    "retentionDays": 90,
    "realtime": true
  }
}
```

## Activity Schema

```typescript
interface Activity {
  id: string;
  timestamp: Date;
  userId?: string;
  service?: string;
  action: string;
  resource: string;
  metadata: Record<string, unknown>;
  level: "info" | "warn" | "error";
}
```

## Dependencies

- Database library (for storage)
- Logger library (for fallback logging)
- Config library

## Services Using It

All services use Activity for audit logging:
- Bliss, Compete, Farmup, Hail, Letease, Proxly, Qihms, Ringly, Synch, Kilimo

## Location

`/home/dave/work/libraries/deno/activity/`
