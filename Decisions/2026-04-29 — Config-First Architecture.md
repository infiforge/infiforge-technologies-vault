---
date: 2026-04-29
tags:
  - decision
  - architecture
  - config
  - environment
---

# 2026-04-29 — Config-First Architecture

## Context

Services were using a mix of .env files, environment variables, and config files. This led to inconsistent configuration management and security issues (committing .env files).

## Decision

Mandate config.json as the single source of truth for all runtime configuration. No .env files allowed. All configuration comes from config.json via the config library.

## Rationale

- **Security**: config.json is in .gitignore, never committed
- **Consistency**: All services use same configuration pattern
- **Flexibility**: Config library supports JSON, TOML, environment variables
- **Type Safety**: Config schema can be validated
- **Reactivity**: Config changes can trigger reconfiguration

## Implementation

### Config Loading Priority

1. config.json (preferred) OR config.toml (never both)
2. .env files (deprecated)
3. Environment variables (terminal)
4. APP_* overrides

### Config Library Features

- Loads from config.json, config.toml, environment variables
- Singleton pattern
- Auto-reload on file change
- Nested key access
- Deep merge configs
- MongoDB config (X509, local, username/password)

### Example config.json

```json
{
  "network": {
    "http": {
      "port": 8100,
      "portRange": {
        "start": 8100,
        "end": 8199
      }
    },
    "ws": { "enabled": true },
    "graphql": { "enabled": true }
  },
  "database": {
    "type": "mongodb",
    "connection": "cloud"
  }
}
```

## Alternatives Considered

1. **.env files only** - Standard practice
   - Rejected: Security risk, often committed accidentally

2. **Environment variables only** - 12-factor app style
   - Rejected: Hard to manage complex configs, no schema

3. **Multiple config sources** - Mix of .env, JSON, env vars
   - Rejected: Confusing, inconsistent across services

## Impact

- All services use config.json
- config.json in .gitignore
- Config library handles all configuration
- No .env files in any service
- Config-driven architecture enables runtime reconfiguration

## Status

✅ Implemented (2026-04-29)
