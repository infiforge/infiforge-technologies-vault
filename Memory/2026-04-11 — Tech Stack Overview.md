---
date: 2026-04-11
updated: 2026-04-11
tags:
  - tech-stack
  - overview
  - architecture
  - deno-libraries
  - flutter-libraries
  - memory-updated
  - lifecycle-pattern
  - network-service
---

# Infiforge Tech Stack Overview

## Last Updated
April 11, 2026

## Recent Updates (2026-04-11)

### New Library Lifecycle Pattern

All Deno libraries now follow a consistent pattern:

```typescript
// 1. Create instance (singleton)
const logger = new LoggerService();

// 2. Initialize with service class
await logger.initialize(this);  // gives access to this.logger, this.config

// 3. Configure (merges with existing)
await logger.configure(this, { logLevel: "debug" });

// 4. Start service
await logger.start();

// 5. Stop gracefully
await logger.stop();

// 6. Restart with optional new config
await logger.restart({ logLevel: "trace" });
```

### Config Service Updates

- `new ConfigService()` - creates instance (auto-loads config)
- `new ConfigService(this)` - creates with service class for `this.config` access
- `config.get(key)` - get config value
- `config.set(key, value)` - set config value
- `config.has(key)` - check if key exists

### Network Service Updates

- Unified HTTP + WebSocket + GraphQL in one service
- Available as: `this.network.http`, `this.network.ws`, `this.network.graphql`
- Network interface support: `"all"`, `"wifi"`, `"lan"`, or custom IPs
- IP resolution: `this.network.localIP`, `this.network.publicIP`

### Libraries Updated

| Library | initialize() | configure() | start() | stop() | restart() |
|---------|--------------|-------------|---------|-------|-----------|
| ConfigService | N/A | N/A | N/A | N/A | reload() |
| LoggerService | ✅ | ✅ | ✅ | ✅ | ✅ |
| DatabaseService | ✅ | ✅ | ✅ | ✅ | ✅ |
| RedisService | ✅ | ✅ | ✅ | ✅ | ✅ |
| SecurityService | ✅ | ✅ | ✅ | ✅ | ✅ |
| NetworkService | ✅ | ✅ | ✅ | ✅ | ✅ |

### Deprecated Libraries (merged into network)

- `websocket/` - merged into `network/`
- `graphql/` - merged into `network/`

---

## Date
April 11, 2026

## Core Philosophy

1. **Multi-database support** - Services can connect to any database based on config.json (MongoDB, PostgreSQL, SQLite, etc.)
2. **Cross-platform** - All services target all platforms (web, mobile, desktop)
3. **Singleton services** - Services are injected as singletons, sharing instances across modules
4. **Config-driven** - Use config.json files, NOT .env files. Never commit config.json to git.
5. **Library Pattern** - Each service has its own server.ts that imports libraries; libraries receive main class instance for logging

---

# DENO LIBRARIES

## Existing Libraries (in /work/libraries/deno/)

### 1. auth - Authentication Library

**Purpose:** All-in-one authentication package imported by ALL services

**Current Status:**
- ✅ JWT token generation (HS256)
- ✅ Email/password sign in/register (basic)
- ✅ OAuth providers (Google, Facebook, Apple, Microsoft, etc.)
- ✅ Refresh token mechanism
- ✅ Middleware (requireAuth, optionalAuth)
- ❌ Password hashing (NOT implemented - should be bcrypt/argon2)
- ❌ Password reset/change
- ❌ Email verification
- ❌ Role-based access control
- ❌ Multi-factor authentication (2FA)
- ❌ Token storage (currently in-memory - should use Redis)
- ❌ Infiforge as identity provider (sign in with Infiforge)

---

### 2. config - Configuration Library

**Purpose:** Singleton config service that reads/holds/updates config for a service

**Current Status:**
- ✅ Loads from config.json, config.toml, environment variables
- ✅ Singleton pattern
- ✅ Auto-reload on file change
- ✅ Nested key access
- ✅ Deep merge configs
- ✅ MongoDB config (partially)
- ❌ Multi-database support
- ❌ Certificate-based MongoDB auth
- ❌ Environment switching (dev/prod)
- ❌ Schema validation
- ❌ Config encryption
- ❌ Reactive (Rx Observables)
- ❌ .env file support
- ❌ Command line argument support

**Config Loading Priority (should be):**
1. config.json (preferred) OR config.toml (never both)
2. .env files
3. Environment variables (terminal)
4. APP_* overrides

---

### 3. database - Database Connection Library

**Purpose:** Singleton service to connect to MULTIPLE databases simultaneously

**Current Status:**
- ✅ Singleton pattern
- ✅ MongoDB connection (basic)
- ✅ User/password authentication
- ✅ Environment detection (cloud/local)
- ✅ Collection access with index creation
- ❌ Multi-database support (only MongoDB)
- ❌ PostgreSQL/MySQL/SQLite/MariaDB support
- ❌ Certificate-based auth (SSL/TLS)
- ❌ Connection pooling
- ❌ Query builder/ORM - NEEDS IMMEDIATE IMPLEMENTATION
- ❌ Database migrations

**Certificate Auth:** Should read from `certs/` folder in backend root

---

### 4. redis - Redis Connection Library

**Purpose:** Redis operations (caching, sessions, pub/sub, rate limiting, multi-instance communication)

**Current Status:**
- ✅ Singleton pattern
- ✅ Basic operations (get, set, del, exists, expire, ttl, keys)
- ✅ Pub/Sub (publish, subscribe)
- ✅ Built-in caching helper with TTL
- ✅ Cache invalidation (pattern-based)
- ❌ TLS/SSL support
- ❌ Redis Sentinel/Cluster support
- ❌ Multiple Redis instances
- ❌ Advanced data types (Lists, Sets, Sorted Sets, Hashes, Streams)

---

### 5. network - Unified Network Library (REBUILT 2026-04-11)

**Purpose:** Unified HTTP + WebSocket + GraphQL service

**Location:** `/work/libraries/deno/network/`

**Current Status (UPDATED):**
- ✅ Unified HTTP/WebSocket/GraphQL service
- ✅ Network interface support: `"all"`, `"wifi"`, `"lan"`, custom IPs
- ✅ IP resolution: `localIP`, `publicIP`, `address`, `publicAddress`
- ✅ Singleton pattern with `getInstance()`
- ✅ Lifecycle: `initialize()`, `configure()`, `start()`, `restart()`, `stop()`

**Properties:**
```typescript
this.network.http      // HTTP service
this.network.ws        // WebSocket service
this.network.graphql   // GraphQL service

this.network.localIP       // "192.168.1.100"
this.network.publicIP      // "203.0.113.1"
this.network.address       // "http://192.168.1.100:8080"
this.network.publicAddress  // "http://203.0.113.1:8080"
this.network.port          // 8080
```

**Network Interfaces:**
```json
{
  "network": {
    "interfaces": "all",  // or "wifi", "lan", ["192.168.1.100"]
    "http": { "port": 8080 },
    "websocket": { "enabled": true },
    "graphql": { "enabled": true }
  }
}
```

---

### 6. websocket - DEPRECATED (merged into network)

**Status:** ✅ MERGED into `deno/network` - 2026-04-11

---

### 6. graphql - DEPRECATED (merge into network)

**Status:** Should be merged into `deno/network` - functionality should be in network library

---

### 7. graphql - DEPRECATED (merged into network)

**Status:** ✅ MERGED into `deno/network` - 2026-04-11

---

### 8. logger - Logging Library

**Purpose:** Standalone logging service

**Architecture:** Each service's main parent class instantiates its own logger instance, then passes it to libraries during configuration

**Current Status:**
- ✅ Singleton pattern
- ✅ Multiple log levels (debug, info, warn, error, critical)
- ✅ Console logging with colors/emojis
- ✅ File logging with rotation
- ✅ Environment detection
- ✅ Log subscribers
- ✅ Instance tracking
- ✅ Metadata support
- ✅ Chainable API
- ❌ Remote logging (Grafana, etc.)
- ❌ Reactive (Rx Observables)

---

### 9. security - Security Library

**Purpose:** Protect services from internet attacks - NEEDS MAJOR IMPROVEMENT

**Current Status:**
- ✅ Basic CORS handling
- ✅ Security headers (helmet)
- ✅ Basic input sanitization
- ✅ Email validation
- ❌ CSRF protection
- ❌ Rate limiting (should integrate with Redis)
- ❌ SQL injection prevention
- ❌ Comprehensive XSS protection
- ❌ IP blocking/whitelisting
- ❌ Advanced encryption (AES, RSA)
- ❌ Industry-standard hashing (bcrypt, argon2)
- ❌ Request validation (JSON schema)

**Required:** Significant work to meet industry standards

---

### 10. static - Static File Serving Library

**Purpose:** Serve static files - www folder, built frontend releases, compressed server releases

**Current Status:**
- ✅ Serves HTML, CSS, JS, images, fonts, videos
- ✅ Extensive MIME types
- ✅ Cache-Control headers
- ✅ Gzip compression
- ✅ Index file support
- ❌ SPA routing support
- ❌ Brotli compression
- ❌ Asset hashing for cache busting

---

### 11. setup - Setup Routes Library

**Purpose:** Provides setup routes for downloading/updating server packages

**Current Status:**
- ✅ Server download routes
- ✅ Unique client obfuscation
- ✅ Checksum verification
- ✅ Setup status checking
- ✅ UniversalRoute compatible
- ❌ Integration with utils library (not created yet)

**Works with:** Flutter `setup` library of same name

---

### 12. routes - UniversalRoute Library

**Purpose:** Provides UniversalRoute interface definition

**Current Status:**
- ✅ UniversalRoute interface definition
- ✅ Health routes creation
- ✅ System routes creation

### 13. utils - Utility Library (NEW!)

**Purpose:** Cross-platform utilities for all Deno services

**Location:** `/work/libraries/deno/utils/`

**Features:**
- Date utilities (format, parse, relative time, timezone)
- String utilities (camelCase, snake_case, slugify, validation)
- File operations (read, write, copy, watch, reactive)
- Process execution (run, spawn, shell commands)
- Platform detection (OS, distribution, root check)
- Network utilities (IP, connectivity, port scanning)
- Service management (systemctl, sc, launchctl)
- Elevation (sudo/pkexec for admin operations)
- Crypto (UUID, hash, AES, HMAC)
- Math (format bytes, currency, clamp)
- Object utilities (deepClone, merge, flatten)
- HTTP client (GET, POST, download with progress)
- Platform paths (app data, cache, logs, downloads)

**Key Functions:**
- `formatDate`, `parseDate`, `relativeTime`
- `isEmail`, `isPhone`, `isUrl`, `isStrongPassword`
- `readFile`, `writeFile`, `watchFile`, `walkDirectory`
- `run`, `runShell`, `spawn`
- `getPlatform`, `isRoot`, `getLinuxDistribution`
- `getLocalIP`, `isOnlineCheck`, `scanPorts`, `waitForPort`
- `isServiceRunning`, `startService`, `stopService`, `createService`
- `elevate`, `requestAdminRestart`
- `generateUUID`, `hashSHA256`, `encryptAES`
- `formatBytes`, `formatCurrency`
- `deepClone`, `deepMerge`, `isEqual`

**Usage:**
```typescript
import { formatDate, isEmail, run, getPlatform, isServiceRunning } from "@infiforge/utils";
```

---

## TO BE CREATED Flutter Libraries

### Flutter Utils Library

See `Flutter Utils Library.md` for full details.

### Additional Flutter Libraries Needed

- Additional auth features to match Deno auth
- Additional network features (more GraphQL, WebSocket)
- More UI components

### Flutter Libraries Renamed (2026-04-11)

| Old Name | New Name | Location |
|---------|----------|----------|
| infiforge_auth | auth | `libraries/flutter/auth/` |
| infiforge_network | network | `libraries/flutter/network/` |
| infiforge_setup | setup | `libraries/flutter/setup/` |

---

## TO BE CREATED Flutter Libraries

### 5. utils - Utility Library (NEW!)

**Purpose:** Cross-platform utilities for all Flutter apps (Android, iOS, Web, Desktop)

**Location:** `/work/libraries/flutter/utils/`

**Features:**
- Date utilities (format, parse, relative time)
- String utilities (camelCase, slugify, validation)
- File operations (read, write, path_provider)
- File picker integration
- Platform detection (OS, distribution)
- Platform operations (service management, paths)
- Process execution and Elevation (desktop only)
- Storage (SharedPreferences + Secure storage)
- Network utilities (connectivity check, HTTP client)
- Dart extensions (String, DateTime, Widget)
- Reactive utilities (ReactiveValue, Debouncer, Throttler)

**Platform Support:**
| Feature | Android | iOS | Web | Desktop |
|---------|---------|-----|-----|---------|
| File Ops | ✅ | ✅ | ✅ | ✅ |
| Platform Detect | ✅ | ✅ | ✅ | ✅ |
| Platform Ops | Limited | Limited | ❌ | ✅ |
| Elevation | ❌ | ❌ | ❌ | ✅ |
| Storage | ✅ | ✅ | ✅ | ✅ |
| Network | ✅ | ✅ | ✅ | ✅ |

**Usage:**
```dart
import 'package:utils/utils.dart';

// Date
final formatted = DateUtils.format(DateTime.now(), 'yyyy-MM-dd');

// Validation
final result = Validators.isEmail('test@example.com');

// Platform
if (PlatformDetect.isDesktop) {
  final isAdmin = await PlatformOps.isAdmin();
}

// Elevation (desktop only)
if (Elevation.isSupported) {
  await Elevation.elevate('systemctl', ['start', 'mongod']);
}

// Storage
await Prefs.setString('token', 'abc123');
await SecureStorageHelper.saveSecureToken('token');

// Reactive
final count = ReactiveValue(0);
count.stream.listen((v) => print('Count: $v'));
```

**Dependencies Required:**
```yaml
dependencies:
  path_provider: ^2.1.0
  file_picker: ^8.0.0
  shared_preferences: ^2.2.0
  flutter_secure_storage: ^9.0.0
  intl: ^0.19.0
```

---

### Additional Flutter Libraries Needed

- Additional auth features to match Deno auth
- Additional network features (more GraphQL, WebSocket)
- More UI components

### Flutter Libraries Renamed (2026-04-11)

| Old Name | New Name | Location |
|---------|----------|----------|
| infiforge_auth | auth | `libraries/flutter/auth/` |
| infiforge_network | network | `libraries/flutter/network/` |
| infiforge_setup | setup | `libraries/flutter/setup/` |

---

# ARCHITECTURE PATTERNS

## Service Architecture (Updated 2026-04-11)

Each service has its own server.ts that uses the new lifecycle pattern:

```typescript
// Service server.ts example
import { NetworkService } from "@infiforge/network";
import { LoggerService } from "@infiforge/logger";
import { ConfigService } from "@infiforge/config";

class MyService {
  public config: ConfigService;
  public logger: LoggerService;
  public network: NetworkService;
  
  constructor() {
    this.config = new ConfigService(this);
    this.logger = new LoggerService(this);
    this.network = new NetworkService(this);
  }
  
  async initialize() {
    await this.config.load();
    
    await this.logger.initialize(this);
    await this.logger.configure(this, this.config.get("logging"));
    await this.logger.start();
    
    await this.network.initialize(this);
    await this.network.configure(this, this.config.get("network"));
    await this.network.start();
  }
}

const service = new MyService();
await service.initialize();
```

### Library Configuration Pattern

```typescript
await service.library.initialize(serviceClass);  // Get access to this.logger, this.config
await service.library.configure(serviceClass, options);  // Merge config
await service.library.start();  // Start service
await service.library.restart(newOptions?);  // Restart
await service.library.stop();  // Stop gracefully
```

### Accessing Services

```typescript
// In your service class
this.logger            // Logger instance
this.config           // Config instance  
this.network           // Network instance
this.network.http     // HTTP service
this.network.ws       // WebSocket service
this.network.graphql  // GraphQL service
```

## UniversalRoute Pattern

Every route supports:
- HTTP REST endpoints
- GraphQL queries/mutations  
- WebSocket real-time communication

---

# KEY RULES

1. ✅ Use Deno for all backend
2. ✅ Use Hono ONLY for HTTP framework
3. ✅ Use config.json for ALL configuration
4. ✅ NEVER commit config.json to git
5. ✅ Use Riverpod with Consumables in Flutter (NOT Bloc)
6. ✅ Use singleton services everywhere
7. ✅ Target ALL platforms (web, mobile, desktop)
8. ✅ All libraries must be reactive (Rx Observables)
9. ✅ Database library must support multiple DB types
10. ✅ MongoDB needs certificate-based auth support
11. ✅ Libraries receive main class instance for logging (MANDATORY)
12. ✅ Use @infiforge/utils library for all services (Deno and Flutter)