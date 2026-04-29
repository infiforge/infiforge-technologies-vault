---
date: 2026-04-28
updated: 2026-04-28
tags:
  - services
  - port-ranges
  - network
  - memory-updated
---

# Infiforge Services - Port Assignments

## Overview
All Infiforge services use the network library which handles HTTP, WebSocket, and GraphQL from a single server. Each service has a designated port range for automatic port allocation.

## Port Assignments

| Service | Location | Port Range | Default Port | Status |
|---------|----------|-----------|-----------|----------|
| Infiforge | internal | 8000-8099 | 8000 | active |
| Bliss | internal | 8100-8199 | 8100 | active |
| Compete | internal | 8200-8299 | 8200 | active |
| Farmup | internal | 8300-8399 | 8300 | active |
| Hail | internal | 8400-8499 | 8400 | active |
| Letease | internal | 8500-8599 | 8500 | active |
| Proxly | internal | 8600-8699 | 8600 | active |
| Qihms | internal | 8700-8799 | 8700 | active |
| Ringly | internal | 8800-8899 | 8800 | active |
| Synch | internal | 8900-8999 | 8900 | active |
| Kilimo | external | 11000-11099 | 11000 | active |

## Network Library Architecture

The network library (`libraries/deno/network/`) provides unified HTTP, WebSocket, and GraphQL services:

### Components
- **HttpService**: Hono-based HTTP server
- **WebSocketService**: Native WebSocket with room support
- **GraphQLService**: GraphQL with playground

### Usage Pattern
```typescript
const networkOptions: NetworkOptions = {
  http: {
    enabled: true,
    port: 8800,
    portRange: { start: 8800, end: 8899 },
  },
  ws: { enabled: true },
  graphql: { enabled: true, playground: true },
};

const network = networkService;
// Get Hono app for route registration
const app = network.http.getApp();

// Register routes
app.get('/api/endpoint', handler);
```

### GraphQL Integration
```typescript
// Using @hono/graphql-server
import { graphqlServer } from 'jsr:@hono/graphql-server'
import { buildSchema } from 'npm:graphql'

const schema = buildSchema(`
  type Query {
    hello: String
  }
`)

app.use('/graphql', graphqlServer({
  schema,
  rootResolver: { hello: () => 'Hello!' },
  graphiql: true
}))
```

### WebSocket Integration
```typescript
// Native WebSocket (built-in)
network.ws.onConnect((client) => {
  client.send({ type: 'welcome' });
});

// Or using socket.io
import { Server } from 'https://deno.land/x/socket_io@0.2.1/mod.ts'
const io = new Server()
```

## Routes Registration Pattern

Each service exports `registerRoutes(serviceClass)` that is called after network starts:

```typescript
// In backend/routes/routes.ts
export async function registerRoutes(service: MyService): Promise<void> {
  const app = service.network.http.getApp();
  
  // Import route arrays from other files
  import { authRoutes } from './auth.ts'
  
  // Register routes
  for (const route of allRoutes) {
    switch (route.method) {
      case 'GET': app.get(route.path, route.handler); break;
      case 'POST': app.post(route.path, route.handler); break;
      // ...
    }
  }
}
```

## Configuration

Port ranges are defined in each service's `config.json`:

```json
{
  "network": {
    "http": {
      "portRange": {
        "start": 8800,
        "end": 8899
      }
    }
  }
}
```

## Updated
- 2026-04-28: Created note with port assignments and network library documentation