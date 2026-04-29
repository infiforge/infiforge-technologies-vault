---
date: 2026-04-11
tags:
  - library
  - flutter
  - utils
  - utilities
---

# @infiforge/utils (Flutter)

## Location
`/work/libraries/flutter/utils/`

## Purpose
Cross-platform utility library for Flutter applications. Works on all platforms (Android, iOS, Web, Windows, macOS, Linux) with desktop-specific features like elevation and service management.

## Structure

```
utils/
├── lib/
│   ├── utils.dart              # Main exports
│   ├── constants.dart          # App constants
│   ├── date/                   # Date utilities
│   │   └── date_utils.dart      # Format, relative time
│   ├── string/                 # String utilities
│   │   ├── string_utils.dart   # Truncate, slugify, etc.
│   │   └── validation.dart     # Email, phone validation
│   ├── file/                   # File operations
│   │   ├── file_ops.dart       # Read, write with dart:io
│   │   └── picker.dart         # File picker integration
│   ├── platform/               # Platform utilities
│   │   ├── platform_detect.dart  # OS detection
│   │   └── platform_ops.dart     # Platform operations
│   ├── process/                # Process execution
│   │   ├── exec.dart           # Process.run wrapper
│   │   └── elevate.dart        # Elevated execution
│   ├── storage/                # Storage utilities
│   │   ├── prefs.dart          # SharedPreferences
│   │   └── secure.dart         # flutter_secure_storage
│   ├── network/                # Network utilities
│   │   └── connectivity.dart  # Internet check
│   ├── extensions/             # Dart extensions
│   │   ├── string_ext.dart     # String extensions
│   │   ├── datetime_ext.dart   # DateTime extensions
│   │   └── widget_ext.dart     # Widget extensions
│   └── reactive/               # Reactive utilities
│       └── rx_utils.dart       # Reactive helpers
```

## Key Functions

### Date
- `DateUtils.format(date, format)` - Format with patterns
- `DateUtils.relativeTime(date)` - "5 minutes ago"
- `DateUtils.startOfDay`, `DateUtils.endOfDay`, etc.
- Extensions: `.formattedShort`, `.formattedLong`, `.relative`

### String
- `.camelCase`, `.snakeCase`, `.kebabCase`, `.pascalCase`, `.titleCase`
- `.slugify`, `.truncate`, `.stripHtml`
- `.isEmail`, `.isUrl`, `.isNumeric`

### Validation
- `Validators.isEmail(value)` - Returns ValidationResult
- `Validators.isPhone`, `Validators.isUrl`, `Validators.isIPv4`
- `Validators.isStrongPassword`
- `ValidationBuilder` for chaining validations

### File
- `FileOps.read(path)`, `FileOps.write(path, content)`
- `FileOps.copy`, `FileOps.move`, `FileOps.delete`
- `FileOps.exists`, `FileOps.stats`, `FileOps.size`
- `DirOps.create`, `DirOps.delete`, `DirOps.list`
- `FilePicker.pickFiles()`, `.pickDirectory()`, `.pickImage()`

### Platform Detection
- `PlatformDetect.current` - Returns PlatformType enum
- `PlatformDetect.isWeb`, `.isMobile`, `.isDesktop`
- `PlatformDetect.isAndroid`, `.isIOS`, `.isWindows`, `.isMacOS`, `.isLinux`
- `LinuxDistro.getDistribution()` - Get distro name
- `LinuxDistro.isDebianBased()`, `.isRedHatBased()`, `.isArchBased()`

### Platform Operations
- `PlatformOps.isAdmin()` - Check if running as admin
- `PlatformOps.getMongoDBPaths()` - Get MongoDB installation paths
- `PlatformOps.getRedisPaths()`, `.getDenoPaths()`
- `PlatformOps.isInternetConnected()`
- `PlatformOps.isMongoDBServiceRunning()`, `.startMongoDBService()`
- `PlatformOps.isRedisServiceRunning()`, `.startRedisService()`

### Process Execution
- `Exec.run(command, args)` - Execute command
- `Exec.runShell(command)` - Run shell command
- `Exec.runStreaming(command, args)` - Streaming output

### Elevation
- `Elevation.elevate(command, args)` - Run with admin privileges
- `Elevation.requestAdminRestart(executablePath)` - Request admin restart
- Implements command whitelist (like QiHMS pattern)
- Desktop only: isDesktop, isMobile checks

### Storage
- `Prefs.init()` - Initialize SharedPreferences
- `Prefs.getString(key)`, `.setString(key, value)`
- `Storage` helper class for common keys
- `SecureStorage` wrapper for flutter_secure_storage
- `SecureStorageHelper` for auth tokens, biometrics

### Network
- `Connectivity.hasInternet()` - Check internet
- `Connectivity.hasWifi()`, `.hasMobileData()`
- `NetworkUtils.getLocalIP()`, `.getPublicIP()`
- `NetworkUtils.isPortAvailable(port)`
- `NetworkUtils.waitForPort(host, port)`
- `HttpClient.get(url)`, `.post(url, body)`

### Extensions
- `StringExt` - .capitalize, .camelCase, .slugify, etc.
- `DateTimeExt` - .formatted, .relative, .isToday, etc.
- `WidgetExt` - .center, .padding, .margin, .gesture

### Reactive
- `ReactiveValue<T>` - Simple reactive value
- `Observable<T>` - Observable subject
- `Subject<T>` - Subject that can emit
- `Debouncer` - Debounce operations
- `Throttler` - Throttle operations
- `RateLimiter` - Rate limit operations
- `ReplaySubject` - Replay last N values

## Usage

```dart
import 'package:utils/utils.dart';

// Date
final formatted = DateUtils.format(DateTime.now(), 'yyyy-MM-dd');

// String
final slug = 'Hello World'.slugify;
final isValid = 'test@example.com'.isEmail;

// Validation
final result = Validators.isEmail('test@example.com');
if (!result.valid) print(result.error);

// File
final content = await FileOps.read('/path/to/file.txt');
await FileOps.write('/path/to/output.txt', 'Hello');

// File Picker
final files = await FilePicker.pickFiles(allowedExtensions: ['pdf']);

// Platform
if (PlatformDetect.isDesktop) {
  final isAdmin = await PlatformOps.isAdmin();
}

// Services
final isRunning = await PlatformOps.isMongoDBServiceRunning();
await PlatformOps.startMongoDBService();

// Elevation (desktop only)
if (Elevation.isSupported) {
  await Elevation.elevate('systemctl', ['start', 'mongod']);
}

// Storage
await Prefs.init();
await Prefs.setString('token', 'abc123');
final token = await Prefs.getString('token');

// Secure Storage
await SecureStorageHelper.saveSecureToken('token');
final token = await SecureStorageHelper.getSecureToken();

// Network
final hasNet = await Connectivity.hasInternet();

// Reactive
final count = ReactiveValue(0);
count.stream.listen((v) => print('Count: $v'));
count.value = 5;

final debouncer = Debouncer(duration: Duration(milliseconds: 300));
debouncer.run(() => print('Debounced action'));
```

## Platform Support

| Feature | Android | iOS | Web | Windows | macOS | Linux |
|---------|---------|-----|-----|---------|-------|-------|
| File Ops | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Picker | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Platform Detect | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Platform Ops | Limited | Limited | ❌ | ✅ | ✅ | ✅ |
| Elevation | ❌ | ❌ | ❌ | ✅ | ✅ | ✅ |
| Storage | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Secure Storage | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Network | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

## Flutter Web Notes

For web, file operations that require native filesystem access will need to communicate with the backend Deno server via API calls. The Flutter utils library can make HTTP requests to the Deno backend for file operations when running in a web context.

## Tree Shakeable

Each module can be imported individually:
```dart
import 'package:utils/utils.dart' show DateUtils;
import 'package:utils/utils.dart' show Validators;
import 'package:utils/utils.dart' show PlatformDetect;
```

## Dependencies Required

Add to pubspec.yaml:
```yaml
dependencies:
  path_provider: ^2.1.0
  file_picker: ^8.0.0
  shared_preferences: ^2.2.0
  flutter_secure_storage: ^9.0.0
  intl: ^0.19.0
```

## Notes

- Works on all Flutter platforms
- Elevation is desktop-only (checks isDesktop first)
- Implements command whitelist for security (like QiHMS)
- Reactive utilities work without Riverpod for simpler cases
- Can integrate with Riverpod for advanced state management