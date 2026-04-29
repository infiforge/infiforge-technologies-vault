---
date: 2026-04-11
tags:
  - library
  - deno
  - utils
  - utilities
---

# @infiforge/utils (Deno)

## Location
`/work/libraries/deno/utils/`

## Purpose
Cross-platform utility library for Deno backend services. Provides common utilities for file operations, process execution, platform detection, network, crypto, and more.

## Structure

```
utils/
├── mod.ts                    # Main exports
├── types.ts                  # Shared types
├── date/                     # Date utilities
│   ├── date_utils.ts         # Format, parse, relative time
│   └── reactive.ts           # Reactive versions
├── string/                   # String utilities
│   ├── string_utils.ts        # Truncate, slugify, camelCase, etc.
│   └── validation.ts          # Email, phone, URL validation
├── file/                     # File system operations
│   ├── file_ops.ts           # Read, write, copy, delete
│   └── dir_ops.ts            # mkdir, rmdir, walk, copy
├── process/                  # Process execution
│   ├── exec.ts               # Process.run, spawn
│   └── elevate.ts            # Sudo/pkexec elevation
├── platform/                 # Platform utilities
│   ├── detect.ts             # OS detection, distribution
│   ├── network.ts            # IP, connectivity, port scan
│   └── services.ts            # Service management
├── crypto/                   # Crypto utilities
│   └── uuid.ts               # UUID, hash, AES encryption
├── math/                     # Math utilities
│   └── number.ts            # Format bytes, currency, clamp
├── object/                   # Object utilities
│   └── object_utils.ts       # Deep clone, merge, flatten
├── http/                     # HTTP client
│   └── client.ts             # REST client, download
└── constants/                # Platform constants
    ├── paths.ts              # Platform-specific paths
    └── mime_types.ts         # MIME type mapping
```

## Key Functions

### Date
- `formatDate(date, format)` - Format with patterns (yyyy, MM, dd, etc.)
- `parseDate(dateStr, format)` - Parse from string
- `relativeTime(date)` - "5 minutes ago"
- `startOfDay`, `endOfDay`, `startOfMonth`, `addDays`, etc.

### String
- `camelCase`, `snakeCase`, `kebabCase`, `pascalCase`, `titleCase`
- `slugify`, `truncate`, `stripHtml`, `escapeHtml`
- `capitalize`, `capitalizeWords`

### Validation
- `isEmail`, `isPhone`, `isUrl`, `isIP`, `isUUID`
- `isStrongPassword`, `isPort`

### File
- `readFile`, `writeFile`, `copyFile`, `deleteFile`
- `exists`, `getStats`, `readJson`, `writeJson`
- `createDirectory`, `deleteDirectory`, `walkDirectory`
- `watchFile`, `watchDirectory` (reactive)
- `getDirectorySize`, `findFiles`, `copyDirectory`

### Process
- `run(command, args)` - Execute command
- `runWithTimeout(command, args, timeout)` - With timeout
- `runShell(command)` - Run shell command
- `spawn(command, args)` - Streaming process

### Platform
- `getPlatform()` - Returns "linux", "windows", "macos"
- `isRoot()` - Check if running as root/admin
- `getLinuxDistribution()` - Get distro (debian, centos, arch)
- `getHomeDirectory`, `getTempDirectory`, `getHostname`

### Network
- `getLocalIP()`, `getPublicIP()`
- `isOnlineCheck()`, `ping(host)`
- `scanPorts(host, start, end)` - Port scanner
- `waitForPort(host, port, timeout)`

### Services
- `isServiceRunning(serviceName)` - Check if running
- `getServiceStatus(serviceName)` - Get detailed status
- `startService`, `stopService`, `restartService`
- `createService`, `deleteService`
- Works on: systemd (Linux), sc (Windows), launchctl (macOS)

### Elevation
- `elevate(command, args)` - Run with admin privileges
- `requestAdminRestart(executablePath)` - Request admin restart
- Implements command whitelist for security

### Crypto
- `generateUUID()` - UUID v4
- `generateSecureToken(length)`
- `hashSHA256`, `hashSHA512`
- `generateHMAC`, `verifyHMAC`
- `encryptAES`, `decryptAES`
- `generateRandomBytes`, `generateRandomNumber`

### Math
- `formatBytes(bytes)` - Format file sizes (1.5 GB)
- `formatCurrency(amount, currency)` - Format currency
- `formatNumber(num, decimals)` - Format with separators
- `clamp`, `round`, `floor`, `ceil`
- `lerp`, `map` (value mapping)

### Object
- `deepClone(obj)` - Deep clone
- `deepMerge(target, source)` - Deep merge
- `flatten(obj)`, `unflatten(flat)` - Flatten nested objects
- `isEqual(obj1, obj2)` - Deep equality check
- `groupBy`, `keyBy`, `pick`, `omit`

### HTTP
- `get`, `post`, `put`, `patch`, `del` - HTTP methods
- `download(url, onProgress)` - Download with progress
- `buildQueryString(params)` - Build URL query string
- `parseQueryString(query)` - Parse query string

### Constants
- `getAppDataDir(appName)` - Platform-specific app data
- `getCacheDir`, `getLogDir`, `getDownloadsDir`
- `getMimeType(filename)` - Get MIME type
- `MIME_TYPES` constant - Full MIME type mapping

## Reactive APIs

Every major function has a reactive version:
- `watchFile`, `watchDirectory` - File system watching
- `createReactiveDateFormatter` - Reactive date formatting

## Usage

```typescript
import { 
  formatDate, 
  isEmail, 
  readFile, 
  run, 
  getPlatform,
  isServiceRunning,
  generateUUID,
  formatBytes
} from "@infiforge/utils";

// Date
const formatted = formatDate(new Date(), "yyyy-MM-dd");

// Validation
const result = isEmail("user@example.com");
if (!result.valid) console.log(result.error);

// File
const content = await readFile("./config.json");
await writeFile("./output.txt", "Hello");

// Process
const result = await run("ls", ["-la"]);

// Platform
const platform = getPlatform(); // "linux", "windows", "macos"

// Services
const isMongoRunning = await isServiceRunning("mongod");

// Crypto
const token = generateUUID();
const hash = await hashSHA256("password");

// Math
const size = formatBytes(1024 * 1024 * 100); // "100 MB"
```

## Platform Support

- **Linux**: Full support (systemd, pkexec, ufw)
- **Windows**: Full support (sc, PowerShell RunAs)
- **macOS**: Full support (launchctl, brew services)

## Tree Shakeable

Each module can be imported individually:
```typescript
import { formatBytes } from "@infiforge/utils/math/number.ts";
import { isEmail } from "@infiforge/utils/string/validation.ts";
```

## Notes

- All functions are synchronous where possible, async where needed
- Implements reactive observables for real-time updates
- Command whitelist for elevation security
- Works on all desktop platforms (Linux, Windows, macOS)