---
date: 2026-04-11
updated: 2026-04-11
tags:
  - project
  - service
  - vpn
  - proxy
  - distributed
---

# Proxly - Distributed VPN & Proxy Service

## Service Details

| Attribute | Value |
|-----------|-------|
| **Name** | Proxly |
| **Type** | Full-stack (Nx monorepo) |
| **Location** | `services/internal/proxly/` |
| **Port Range** | 8600-8699 |
| **Package** | com.infiforge.proxly |

## Description

Distributed VPN and proxy service that allows each device it is installed on to act as a hub for other clients to connect to. Supports multiple protocols including WireGuard, OpenVPN, IPSec, HTTPS, SOCKS4, and SOCKS5.

## Architecture

```
proxly/
├── backend/          # Deno API server
├── frontend/         # Flutter cross-platform app
├── extension/        # Browser extension
└── nx.json          # Nx workspace
```

---

## Backend (Deno)

### Libraries Used (11 total)

All from `~/work/libraries/deno`:

| # | Library | Purpose |
|---|---------|---------|
| 1 | `@infiforge/auth` | JWT creation/verification, OAuth middleware |
| 2 | `@infiforge/config` | Configuration loading (supports X509, local, username/password MongoDB) |
| 3 | `@infiforge/database` | MongoDB connection management |
| 4 | `@infiforge/logger` | Structured logging |
| 5 | `@infiforge/network` | **HTTP + WebSocket + GraphQL combined** - contains hono internally |
| 6 | `@infiforge/redis` | Cache, sessions, pub/sub |
| 7 | `@infiforge/routes` | Universal routes helpers |
| 8 | `@infiforge/security` | Encryption, CORS |
| 9 | `@infiforge/setup` | Setup utilities |
| 10 | `@infiforge/static` | Static file serving |
| 11 | `rxjs` (npm:) | Reactive Observable streams |

**Note:** WebSocket and GraphQL libraries were removed - their functionality merged into network library.

### Server.ts Pattern

```typescript
import { NetworkService } from "@infiforge/network";

export class Proxly {
  public logger!: LoggerService;
  public config!: ConfigService;
  public database!: DatabaseService;
  public network!: NetworkService;

  constructor() {
    this.network = NetworkService.getInstance();
  }

  async initialize(options: ProxlyOptions = {}): Promise<void> {
    this.config = new ConfigService(this);
    await this.config.load(options.configPath);
    
    this.logger = new LoggerService();
    await this.logger.configure(this, { serviceName: "proxly" });
    
    await this.network.initialize(this);
    await this.network.configure(this, {
      http: { port: options.port || 8600, enabled: true },
      ws: { enabled: true },
      graphql: { enabled: true },
    });
  }

  static async launch(port?: number): Promise<Proxly> {
    const proxly = new Proxly();
    await proxly.initialize({ port });
    await proxly.start();
    return proxly;
  }

  async start(): Promise<void> {
    await this.network.start();
  }
}
```

### Key Patterns

1. **No direct hono import** - comes via network library
2. **GraphQL via network** - network.graphql handles GraphQL
3. **Library configure pattern** - each library has `.configure(proxly, options)` method
4. **Static launch function** - `Proxly.launch(port)` initializes and starts

### Universal Routes

All routes support HTTP + WebSocket + GraphQL:

```typescript
new UniversalRoute({
  accepts: [AllowedRouteTypes.all],
  paths: { http: "/api/hubs", graphql: "hubs", ws: "hubs" },
  method: UniversalRouteMethod.get,
  async func(payload, ctx) {
    return { success: true, data: hubService.getHubs() };
  },
}),
```

### Backend Folder Structure

```
backend/
├── server.ts
├── deno.json
├── config.json
├── routes/
│   ├── routes.ts
│   ├── auth.ts
│   ├── hubs.ts
│   ├── clients.ts
│   ├── vpn.ts
│   └── proxy.ts
├── services/
│   ├── hub-service.ts        # Singleton + Rx provider
│   ├── connection-service.ts
│   ├── vpn/                  # Protocol services
│   │   ├── wireguard.ts
│   │   ├── openvpn.ts
│   │   └── ipsec.ts
│   └── proxy/                # Proxy services
│       ├── http.ts
│       ├── socks4.ts
│       └── socks5.ts
├── graphql/
├── interfaces/
└── www/
```

---

## Frontend (Flutter)

### Libraries Used

From `~/work/libraries/flutter`:

| # | Library | Purpose |
|---|---------|---------|
| 1 | `infiforge_auth` | OAuth (Google, Microsoft, Apple), JWT, biometric auth |
| 2 | `infiforge_network` | HTTP, WebSocket, GraphQL clients |
| 3 | `infiforge_setup` | Hub setup wizard |
| 4 | `uxage` | Onboarding, feature tours |
| 5 | `flutter_riverpod` | State management |
| 6 | `rxdart` | Reactive streams |

### Pages Required (10)

| Page | Source | Wrapper |
|------|--------|---------|
| **Intro** | Custom (`pages/app/intro.dart`) | None |
| **Auth** | `import AuthPage from infiforge_auth` | **Direct import - no wrapper** |
| **Home** | Custom with switchable screens | Dashboard, Hubs, Clients, Settings |
| **Setup** | `import SetupPage from setup` | **Direct import - no wrapper** |
| **Website** | Custom (`pages/website/website_page.dart`) | None |
| **TOS** | Custom (`pages/website/terms_of_service.dart`) | None |
| **Privacy** | Custom (`pages/website/privacy_policy.dart`) | None |
| **About** | Custom (`pages/website/about_us_screen.dart`) | None |
| **Admin Portal** | Custom (`pages/admin/dashboard_screen.dart`) | None |
| **Splash** | Custom (for platforms without native splash) | None |

### Frontend Folder Structure

```
frontend/lib/
├── main.dart
├── core/
│   ├── router/
│   │   └── platform_router.dart
│   ├── config/
│   │   └── app_config.dart
│   └── theme/
│       └── app_theme.dart
├── pages/                           # NOT features/ folder
│   ├── app/
│   │   ├── intro.dart
│   │   └── home/
│   │       ├── home_screen.dart
│   │       ├── dashboard_screen.dart
│   │       ├── hubs_screen.dart
│   │       ├── clients_screen.dart
│   │       └── settings_screen.dart
│   ├── auth/                        # Uses infiforge_auth directly
│   ├── admin/
│   │   └── screens/
│   ├── setup/                       # Uses setup directly
│   └── website/
│       └── pages/
└── shared/
    ├── services/                    # Singleton services (NO providers folder)
    │   ├── auth_service.dart
    │   ├── hub_service.dart         # Singleton + hubServiceProvider
    │   ├── connection_service.dart
    │   └── network_service.dart
    ├── models/
    └── widgets/
```

### Key Patterns

1. **Pages folder** - NOT features folder
2. **No providers folder** - providers derived from singleton services
3. **Direct imports** - AuthPage and SetupPage without wrappers

### Singleton + Provider Pattern

```dart
class HubService {
  static final HubService _instance = HubService._internal();
  factory HubService() => _instance;
  HubService._internal();
  
  final _hubs$ = BehaviorSubject<List<Hub>>([]);
  Stream<List<Hub>> get hubs$ => _hubs$.stream;
}

export final hubServiceProvider = Provider<HubService>((ref) => HubService());
export final hubsStreamProvider = StreamProvider<List<Hub>>((ref) {
  return ref.watch(hubServiceProvider).hubs$;
});
```

---

## Database Collections

| Collection | Purpose |
|------------|---------|
| `hubs` | Registered hub devices |
| `clients` | Connected clients |
| `connections` | Active connections |
| `users` | User accounts |
| `config` | Service configuration |
| `logs` | Activity logs |
| `metrics` | Usage stats |

## MongoDB Configuration

- **Production:** MongoDB Atlas with X509 certificate
- **Development:** Local MongoDB
- Configured via config.json using `@infiforge/config`

---

## Browser Extension

```
extension/
├── manifest.json
├── background.js
├── content.js
└── popup.html
```

Supports Chrome, Firefox, Edge, and other browsers.

---

## Protocol Services

Each protocol as dedicated singleton service:
- `services/vpn/wireguard.ts` - WireGuard
- `services/vpn/openvpn.ts` - OpenVPN
- `services/vpn/ipsec.ts` - IPSec
- `services/proxy/http.ts` - HTTP proxy
- `services/proxy/socks4.ts` - SOCKS4
- `services/proxy/socks5.ts` - SOCKS5

---

## Development Commands

```bash
# Backend
deno run --allow-all backend/server.ts

# Frontend
cd frontend && flutter run

# Build
cd frontend && flutter build web
```

---

## Status

- ✅ Active service
- ✅ Nx monorepo structure
- ✅ ServiceInstance base class pattern implemented
- ✅ UniversalRoute pattern implemented
- ✅ Port configuration fixed (8600-8699)
- ✅ Tested and working (2026-04-29)
- Note: Comprehensive VPN/proxy service with 11 Deno libraries

## Related Decisions

- Using Nx workspace (following existing services)
- Using Riverpod with consumables (NOT providers folder)
- Using rxdart in Flutter, rxjs in Deno
- Direct library imports for AuthPage and SetupPage
- Pages folder instead of features
- Universal routes supporting HTTP + WS + GraphQL

## Release Information

> [!info] Added: 2026-04-29

- GitLab: https://gitlab.com/infiforge1/proxly
- GitHub: https://github.com/infiforge/proxly
- Path: `~/work/services/internal/proxly`
- Push: `git push all main`