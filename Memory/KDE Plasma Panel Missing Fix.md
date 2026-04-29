---
date: 2026-04-29
updated: 2026-04-29
tags:
  - memory-updated
  - kde
  - plasma
  - linux
  - fix
---

# KDE Plasma Panel Missing Fix

## Problem
KDE Plasma panel (taskbar) not visible at bottom of screen.

## Solution

**Working command:**
```bash
systemctl restart --user plasma-plasmashell.service
```

## Alternative Commands

If systemctl not available:
```bash
plasmashell --replace & disown
```

Or:
```bash
killall plasmashell && plasmashell &
```

## References
- KDE Plasma 6 uses systemd user service for plasmashell
- Fixed via searching KDE forums and KDE Discuss

## Updated
- 2026-04-29: Documented fix from successful session