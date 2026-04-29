---
date: 2026-04-29
updated: 2026-04-29
tags:
  - library
  - deno
  - system-utils
  - utilities
---

# System Utils Library

## Overview

System Utils library provides cross-platform system utilities for Deno services. Includes process management, service control, platform detection, and system information.

## Purpose

- Provide cross-platform system operations
- Enable service management (systemd, launchctl, sc)
- Support platform detection and distribution info
- Provide elevation and privilege management
- Enable system-level operations

## Key Features

- Service management (systemd, launchctl, sc)
- Platform detection (Linux, Windows, macOS)
- Linux distribution detection (Debian, Red Hat, Arch)
- Process execution and elevation
- System information gathering
- Command whitelist for security

## Module Pattern

```typescript
initialize(): Promise<void>
configure(instance: ServiceInstance, options: SystemUtilsOptions): Promise<void>
start(instance?: ServiceInstance): Promise<void>
stop(): Promise<void>
restart(): Promise<void>
```

## Usage

```typescript
import { SystemUtilsModule } from "@infiforge/system-utils";

// Platform detection
const platform = await this.systemUtilsModule.getPlatform();
// Returns: "linux", "windows", "macos"

// Linux distribution
if (platform === "linux") {
  const distro = await this.systemUtilsModule.getLinuxDistribution();
  // Returns: "debian", "ubuntu", "redhat", "arch", etc.
}

// Service management
const isRunning = await this.systemUtilsModule.isServiceRunning("mongod");
await this.systemUtilsModule.startService("mongod");

// Process execution
const result = await this.systemUtilsModule.run("ls", ["-la"]);

// Elevation (desktop only)
if (await this.systemUtilsModule.isDesktop()) {
  await this.systemUtilsModule.elevate("systemctl", ["start", "mongod"]);
}
```

## Configuration Options

```json
{
  "system-utils": {
    "enabled": true,
    "elevation": {
      "commandWhitelist": ["systemctl", "service", "launchctl", "sc"]
    }
  }
}
```

## Platform Support

- **Linux**: Full support (systemd, pkexec, ufw)
- **Windows**: Full support (sc, PowerShell RunAs)
- **macOS**: Full support (launchctl, brew services)

## Dependencies

- Deno standard library
- Platform-specific commands (systemd, launchctl, sc)

## Services Using It

All services use SystemUtils for system operations:
- Bliss, Compete, Farmup, Hail, Letease, Proxly, Qihms, Ringly, Synch, Kilimo

## Location

`/home/dave/work/libraries/deno/system-utils/`
