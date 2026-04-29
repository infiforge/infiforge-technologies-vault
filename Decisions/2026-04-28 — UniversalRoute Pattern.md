---
date: 2026-04-29
tags:
  - decision
  - architecture
  - universal-route
  - routes
---

# 2026-04-28 — UniversalRoute Pattern

## Context

Services had inconsistent route definitions across HTTP, WebSocket, and GraphQL. Each service defined its own route interfaces, leading to duplication and maintenance overhead.

## Decision

Standardized all service routes to use UniversalRoute pattern from @infiforge/routes library, supporting HTTP, WebSocket, and GraphQL from a single route definition.

## Rationale

- **DRY**: Define route once, accessible via HTTP, WS, and GraphQL
- **Consistency**: All services use same route interface
- **Type Safety**: Shared interfaces prevent mismatches
- **Error Handling**: Standardized UniversalRouteResponse format
- **GraphQL Support**: Each route has graphqlTypeDefs that mirrors the func

## Implementation

### UniversalRoute Interface

```typescript
interface UniversalRoute {
  accepts: AllowedRouteTypes | AllowedRouteTypes[];
  paths: { http?: string; graphql?: string; ws?: string };
  method: UniversalRouteMethod;
  description: string;
  graphqlTypeDefs: string;  // REQUIRED - mirrors the func
  func: (input: Record<string, unknown>, context: RouteContext) => Promise<UniversalRouteResponse>;
}
```

### Key Requirements

1. **Route Interface**: Use AllowedRouteTypes, UniversalRoute, UniversalRouteMethod from @infiforge/routes
2. **GraphQL Support**: Each route MUST have graphqlTypeDefs that mirrors the func
3. **AppRoutes Pattern**: Each service's routes.ts exports AppRoutes class that collects all route files
4. **Handler**: func is the handler regardless of HTTP/WS/GraphQL access
5. **Error Handling**: Return { success: false, errorMessage: string, error: Error } via UniversalRouteResponse
6. **Static Routes**: Handled by static library, NOT in service route files

### Example

```typescript
new UniversalRoute({
  accepts: [AllowedRouteTypes.all],
  paths: { http: '/health', graphql: 'Health', ws: 'health' },
  method: UniversalRouteMethod.get,
  description: 'Health check',
  graphqlTypeDefs: `
    type HealthResponse {
      success: Boolean!
      status: String!
    }
    type Query {
      Health: HealthResponse!
    }
  `,
  async func() {
    return { success: true, status: 'OK' };
  },
})
```

## Alternatives Considered

1. **Separate route definitions** - HTTP, WS, GraphQL defined separately
   - Rejected: Duplication, maintenance overhead

2. **Per-service route interfaces** - Each service defines its own
   - Rejected: Inconsistent, no type safety across services

3. **No GraphQL support** - HTTP and WS only
   - Rejected: GraphQL is core to Infiforge architecture

## Impact

- All services use UniversalRoute pattern
- Single route definition accessible via HTTP, WS, GraphQL
- Standardized error handling across all services
- AppRoutes class pattern for route collection
- Deleted per-service interface files

## Status

✅ Implemented and tested (2026-04-28)
