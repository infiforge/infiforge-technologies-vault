---
title: Infiforge Infrastructure
date: 2026-04-17
tags:
  - infrastructure
  - infiforge
  - tailscale
  - caddy
status: active
---

# Infiforge Infrastructure Setup

## Overview

Complete infrastructure setup for accessing Infiforge services via multiple access methods: phone (SSH tunnel), Tailscale IP, Tailscale Funnel (public internet), and local.

## Port Ranges

| Category | Range | Services |
|----------|-------|----------|
| Internal Services | 8000-8999 | infiforge, bliss, compete, farmup, hail, letease, proxly, qihms, ringly, synch |
| External Services | 11000-11999 | kilimo |
| System Services | Fixed | openclaw (18789), opencode (9200), n8n (5678), ollama (11434), redis (6379), mongodb (27017) |

## Access Methods

### 1. Phone Access (via SSH Tunnel)
Services accessible on phone via `http://<service>.infiforge`:
- `http://infiforge.infiforge` → infiforge:8000
- `http://bliss.infiforge` → bliss:8100
- `http://compete.infiforge` → compete:8200
- `http://farmup.infiforge` → farmup:8300
- `http://hail.infiforge` → hail:8400
- `http://letease.infiforge` → letease:8500
- `http://proxly.infiforge` → proxly:8600
- `http://qihms.infiforge` → qihms:8700
- `http://ringly.infiforge` → ringly:8800
- `http://synch.infiforge` → synch:8900
- `http://kilimo.infiforge` → kilimo:11000
- `http://openclaw.infiforge` → openclaw:18789
- `http://opencode.infiforge` → opencode:9200
- `http://n8n.infiforge` → n8n:5678

### 2. Tailnet IP Access
- `http://100.81.250.42/` → infiforge:8000 (default)
- `http://100.81.250.42/n8n` → n8n:5678
- `http://100.81.250.42:9200` → opencode:9200

### 3. Tailscale Funnel (Public Internet)
- `https://infiforge.tail4703d5.ts.net/` → infiforge:8000
- `https://infiforge.tail4703d5.ts.net/n8n` → n8n:5678

## Services

### Working Services (10)
| Service | Port | Port Range | Location | Status |
|---------|------|------------|----------|--------|
| infiforge | 8000 | 8000-8099 | internal/infiforge/backend | ✅ |
| bliss | 8100 | 8100-8199 | internal/bliss/backend | ✅ |
| compete | 8200 | 8200-8299 | internal/compete/backend | ✅ |
| hail | 8400 | 8400-8499 | internal/hail/backend | ✅ |
| letease | 8500 | 8500-8599 | internal/letease/backend | ✅ |
| qihms | 8700 | 8700-8799 | internal/qihms/backend | ✅ |
| ringly | 8800 | 8800-8899 | internal/ringly/backend | ✅ |
| openclaw | 18789 | - | systemd | ✅ |
| opencode | 9200 | - | systemd | ✅ |
| n8n | 5678 | - | Docker | ✅ |

### Services with Code Issues (4)
| Service | Port | Port Range | Issue |
|---------|------|------------|-------|
| farmup | 8300 | 8300-8399 | Import error in accounts.ts |
| proxly | 8600 | 8600-8699 | Not binding to port |
| synch | 8900 | 8900-8999 | Mongo import not found |
| kilimo | 11000 | 11000-11099 | Import map issue |

## Configuration Files

### Caddy Configuration
- **Template:** `/home/dave/work/Caddyfile`
- **Active:** `/etc/caddy/Caddyfile`
- Uses hostname-based routing for phone access and path-based for tailnet/funnel

### Systemd Services
- **Templates:** `/home/dave/work/systemd/*.service`
- **Installed:** `/etc/systemd/system/`
- All services use Deno at `/home/dave/.deno/bin/deno`

### Phone SSH Tunnels
- **File:** `~/.termux/boot/ssh-tunnels` on phone
- Single tunnel: port 80 → Caddy → routes by hostname

### Tailscale
- Funnel enabled on port 80
- tailscale-funnel.service enabled at boot
- URL: `https://infiforge.tail4703d5.ts.net`

## Key Commands

```bash
# Start services
sudo systemctl start infiforge@8000 bliss@8100 compete@8200

# Check status
systemctl status infiforge@8000

# Reload Caddy
sudo systemctl reload caddy

# Check funnel
sudo tailscale funnel status

# SSH to phone
ssh phone
```

## Related
- [[Tailscale Setup]]
- [[Caddy Reverse Proxy]]
- [[Service Deployment]]