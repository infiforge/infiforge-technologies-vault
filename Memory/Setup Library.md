---
date: 2026-04-29
updated: 2026-04-29
tags:
  - library
  - deno
  - setup
  - installation
---

# Setup Library

## Overview

Setup library provides setup routes and utilities for downloading and updating server packages. Works with Flutter setup library for desktop installation.

## Purpose

- Provide setup routes for downloading server packages
- Enable server package updates
- Support unique client obfuscation
- Provide checksum verification
- Enable setup status checking

## Key Features

- Server download routes
- Unique client obfuscation
- Checksum verification
- Setup status checking
- UniversalRoute compatible
- Works with Flutter setup library

## Module Pattern

```typescript
initialize(): Promise<void>
configure(instance: ServiceInstance, options: SetupOptions): Promise<void>
start(instance?: ServiceInstance): Promise<void>
stop(): Promise<void>
restart(): Promise<void>
```

## Usage

```typescript
import { SetupModule } from "@infiforge/setup";

// In service initialize()
this.setupModule = new SetupModule();
await this.setupModule.initialize();
await this.setupModule.configure(this, {
  packagePath: "./packages",
  checksumAlgorithm: "sha256"
});

// Setup routes are automatically registered
// GET /setup/download - Download server package
// GET /setup/status - Check setup status
// GET /setup/version - Get current version
```

## Configuration Options

```json
{
  "setup": {
    "enabled": true,
    "packagePath": "./packages",
    "checksumAlgorithm": "sha256",
    "version": "1.0.0"
  }
}
```

## Setup Routes

- `GET /setup/download` - Download server package with checksum
- `GET /setup/status` - Check if setup is complete
- `GET /setup/version` - Get current package version
- `POST /setup/verify` - Verify package checksum

## Flutter Integration

Works with Flutter setup library (`infiforge_setup`) for:
- Desktop installation
- Package download
- Setup wizard
- Auto-updates

## Dependencies

- Static library (for serving packages)
- Routes library (UniversalRoute pattern)
- Config library

## Services Using It

All services use Setup for package distribution:
- Bliss, Compete, Farmup, Hail, Letease, Proxly, Qihms, Ringly, Synch, Kilimo

## Location

`/home/dave/work/libraries/deno/setup/`
