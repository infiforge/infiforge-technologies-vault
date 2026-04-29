---
date: 2026-04-29
tags:
  - area
  - devops
  - ci-cd
  - automation
---

# DevOps

## Focus

DevOps practices for Infiforge services including CI/CD, deployment automation, and service management.

## Related Projects

All 11 services use DevOps practices:
- [[Bliss — Hotel Management System]]
- [[Compete — School Management System]]
- [[Farmup — Farm Management System]]
- [[Hail — Skill Sharing Marketplace]]
- [[Infiforge — Main Orchestration Service]]
- [[Letease — File Sharing]]
- [[Proxly — Distributed VPN Proxy Service]]
- [[QiHMS — Hospital Management System]]
- [[Ringly — Call Attribution]]
- [[Synch — File Sharing]]
- [[Kilimo — Farm Management System]]

## Related Libraries

- [[System Utils Library]] (service management)
- [[Setup Library]] (package distribution)

## CI/CD Pipeline

### GitLab CI

Each service has `.gitlab-ci.yml` that:
1. Builds Flutter app for Linux (x64)
2. Creates `.tar.gz` archive
3. Creates `.deb` package
4. On tag push: creates GitLab release

### Git Remotes

| Remote | URL | Purpose |
|--------|-----|---------|
| `origin` | git@gitlab.com:infiforge1/[service].git | Primary (GitLab) |
| `github` | git@github.com:infiforge/[service].git | Secondary |
| `all` | git@gitlab.com + git@github.com | Push to both |

### Push Commands

```bash
git add .
git commit -m "Update"
git push all main

# Create release tag
git tag flutter-v1.0.0
git push all flutter-v1.0.0
```

## Service Management

### Linux (systemd)

```bash
systemctl start [service]
systemctl stop [service]
systemctl restart [service]
systemctl status [service]
```

### macOS (launchctl)

```bash
brew services start [service]
brew services stop [service]
brew services restart [service]
```

### Windows (sc)

```powershell
sc start [service]
sc stop [service]
sc query [service]
```

## Active Work

- ServiceInstance refactoring (completed 2026-04-29)
- CI/CD pipeline setup (existing)
