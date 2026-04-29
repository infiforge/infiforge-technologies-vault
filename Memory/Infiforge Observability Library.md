# @infiforge/observability

Observability library for Infiforge services - OpenTelemetry + Prometheus integration.

## Overview

The `@infiforge/observability` library provides unified observability for all Infiforge services including:
- OpenTelemetry for distributed tracing
- Prometheus metrics with RED pattern
- Health endpoints (/health, /ready, /metrics)
- HTTP middleware for automatic instrumentation

## Installation

```typescript
import { ObservabilityModule } from "@infiforge/observability";
```

Library location: `/home/dave/work/libraries/deno/observability/`

## Configuration

### Full Configuration Options

```json
{
  "observability": {
    "enabled": true,
    "serviceName": "auto",
    "version": "1.0.0",
    "environment": "development",
    
    "otel": {
      "enabled": true,
      "exporter": "otlp",
      "collectorEndpoint": "",
      "collectorMode": false
    },
    
    "prometheus": {
      "enabled": true,
      "scrapePort": 9464,
      "scrapePath": "/metrics",
      "defaultMetricsInterval": 10000
    },
    
    "health": {
      "livenessPath": "/health",
      "readinessPath": "/ready",
      "metricsPath": "/metrics",
      "includeDependencies": false,
      "dependencyTimeout": 5000
    },
    
    "metrics": {
      "enabled": true,
      "custom": {},
      "redMetrics": {
        "enabled": true,
        "excludePaths": ["/health", "/ready", "/metrics", "/favicon.ico"]
      }
    }
  }
}
```

### Configuration Details

| Option | Type | Description | Default |
|-------|------|-------------|---------|
| `enabled` | boolean | Enable/disable observability | `true` |
| `serviceName` | string | Service name ("auto" picks from config) | `"auto"` |
| `version` | string | Service version | `"1.0.0"` |
| `environment` | string | dev/staging/production | `"development"` |

### OpenTelemetry (otel)

| Option | Type | Description | Default |
|-------|------|-------------|---------|
| `enabled` | boolean | Enable OTel | `true` |
| `exporter` | string | "otlp" \| "console" \| "none" | `"otlp"` |
| `collectorEndpoint` | string | Custom OTLP endpoint | `""` |
| `collectorMode` | boolean | Use collector vs direct | `false` |

### Prometheus (prometheus)

| Option | Type | Description | Default |
|-------|------|-------------|---------|
| `enabled` | boolean | Enable Prometheus | `true` |
| `scrapePort` | number | Metrics scrape port | `9464` |
| `scrapePath` | string | Metrics path | `"/metrics"` |
| `defaultMetricsInterval` | number | Collection interval (ms) | `10000` |

### Health Endpoints (health)

| Option | Type | Description | Default |
|-------|------|-------------|---------|
| `livenessPath` | string | Liveness probe path | `"/health"` |
| `readinessPath` | string | Readiness probe path | `"/ready"` |
| `metricsPath` | string | Metrics path | `"/metrics"` |
| `includeDependencies` | boolean | Check dependencies | `false` |
| `dependencyTimeout` | number | Check timeout (ms) | `5000` |

### Metrics (metrics)

| Option | Type | Description | Default |
|-------|------|-------------|---------|
| `enabled` | boolean | Enable metrics | `true` |
| `custom` | object | Custom metrics definitions | `{}` |
| `redMetrics.enabled` | boolean | Enable RED metrics | `true` |
| `redMetrics.excludePaths` | string[] | Paths to exclude | see below |

Default RED exclusions:
- `/health`
- `/ready`
- `/metrics`
- `/favicon.ico`

## Service Integration

### Adding to a Service

```typescript
// 1. Import
import { ObservabilityModule } from "@infiforge/observability";

// 2. Add property
public observabilityModule!: ObservabilityModule;

// 3. In initialize()
this.observabilityModule = new ObservabilityModule();
await this.observabilityModule.initialize();

// 4. In configure()
await this.observabilityModule.configure(this, latestConfig.get("observability"));

// 5. In start()
await this.observabilityModule.start(this.network);

// 6. In stop()
await this.observabilityModule.stop();
```

### Module Order

Observability should be at position 13 in canonical order:
1. config → 2. logger → 3. redis → 4. network → 5. auth → 6. static → 7. activity → 8. ai → 9. routes → 10. isc → 11. setup → 12. system-utils → 13. **observability** → 14. database

## RED Metrics Pattern

The library auto-creates RED metrics:

### Request Rate
```promql
rate(http_requests_total[5m])
```

### Error Rate
```promql
rate(http_requests_total{status_code=~"5.."}[5m])
```

### Duration (p50, p95, p99)
```promql
histogram_quantile(0.95, rate(http_request_duration_seconds_bucket[5m]))
```

### Metrics Created

| Metric | Type | Labels |
|--------|------|--------|
| `http_request_duration_seconds` | histogram | method, route, status_code |
| `http_requests_total` | counter | method, route, status_code |
| `http_requests_in_progress` | gauge | method, route |

## HTTP Middleware

The middleware automatically:
1. Creates spans for each request
2. Records request duration
3. Tracks request counts
4. Injects trace context into responses

### Excluding Paths

 Paths can be excluded via `excludePaths` in config:
 
 ```json
 "metrics": {
   "redMetrics": {
     "excludePaths": ["/health", "/healthz", "/metrics", "/favicon.ico"]
   }
 }
 ```

## Custom Metrics

Define custom metrics in config:

```json
"metrics": {
  "custom": {
    "business_orders_total": {
      "type": "counter",
      "description": "Total orders processed",
      "labels": ["status"]
    },
    "queue_depth": {
      "type": "gauge",
      "description": "Current queue depth",
      "labels": ["queue_name"]
    }
  }
}
```

## Endpoints

Each service exposes:

| Endpoint | Purpose |
|----------|---------|
| `GET /health` | Liveness probe |
| `GET /ready` | Readiness probe (with dependency checks) |
| `GET /metrics` | Prometheus scrape endpoint |

## Environment Variables (OTel)

The library respects standard OTEL environment variables:
- `OTEL_EXPORTER_OTLP_ENDPOINT`
- `OTEL_SERVICE_NAME`
- `OTEL_SERVICE_VERSION`
- `OTEL_ENVIRONMENT`
- `OTEL_DENO=true` (for Deno 2.2+ built-in OTel)

## Related

- [[Infiforge Services]] - Service list
- [[Infiforge Infrastructure]] - Infrastructure overview
- [[Deno Utils Library]] - Deno utilities
- Workplan: [[workplan.md]] - Implementation workplan