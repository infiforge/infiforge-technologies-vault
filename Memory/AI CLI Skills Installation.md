---
title: AI CLI Skills Installation
date: 2026-04-16
tags:
  - ai
  - tools
  - skills
  - opencode
  - claude-code
  - obsidian
aliases:
  - AI Skills Setup
  - CLI AI Skills
---

# AI CLI Skills Installation

Installed a comprehensive set of AI coding agent skills on `/mnt/data/ai-skills/` for cross-platform access from Linux and Windows.

> [!info] Central Location
> Skills are stored on the shared `/mnt/data/` partition so they persist across Linux/Windows reinstalls.

## Skills Overview

Installed **32 skills** across three collections:

| Collection | Count | Purpose |
|------------|-------|---------|
| [[Superpowers]] | 13 | Development workflow |
| [[Obsidian Skills]] | 5 | Vault management |
| [[Obsidian Vault Agent]] | 12 | AI knowledge management |

## Symlinks Created

All CLI tools now point to `/mnt/data/ai-skills/skills/`:

```bash
~/.config/opencode/skills/  → /mnt/data/ai-skills/skills/
~/.claude/skills/           → /mnt/data/ai-skills/skills/
~/.gemini/skills/           → /mnt/data/ai-skills/skills/
~/.kilo/skills/            → /mnt/data/ai-skills/skills/
~/.kimi/skills/            → /mnt/data/ai-skills/skills/
~/.codex/skills/           → /mnt/data/ai-skills/skills/
~/.agents/skills/          → /mnt/data/ai-skills/skills/
```

## Superpowers Skills

Structured development workflow following TDD principles:

- [[brainstorming]] - Requirements exploration before coding
- [[test-driven-development]] - RED-GREEN-REFACTOR enforcement
- [[systematic-debugging]] - Root cause analysis before fixes
- [[verification-before-completion]] - Evidence before claims
- [[writing-plans]] - Bite-sized implementation plans
- [[executing-plans]] - Plan execution with checkpoints
- [[subagent-driven-development]] - Parallel task execution
- [[dispatching-parallel-agents]] - Concurrent work
- [[requesting-code-review]] - Pre-merge verification
- [[receiving-code-review]] - Feedback handling
- [[using-git-worktrees]] - Isolated workspaces
- [[finishing-a-development-branch]] - Merge decision
- [[using-superpowers]] - Meta skill for discovery
- [[writing-skills]] - Create new skills

## Obsidian Skills

Vault management skills from [[kepano/obsidian-skills]]:

- [[obsidian-markdown]] - Wikilinks, embeds, callouts, properties
- [[obsidian-bases]] - Structured data (.base files)
- [[json-canvas]] - Visual thinking (.canvas files)
- [[obsidian-cli]] - Vault operations via CLI
- [[defuddle]] - Extract clean markdown from web

## Obsidian Vault Agent

AI-powered knowledge management from [[tuan3w/obsidian-vault-agent]]:

- [[init]] - Initialize Zettelkasten vault structure
- [[course]] - Process course URLs into structured notes
- [[book-analyzer]] - Extract and analyze book content
- [[youtube]] - Create notes from YouTube videos
- [[process]] - Learning science processing pipeline
- [[synthesize]] - Cross-domain knowledge synthesis
- [[research]] - Multi-pass research with web + vault
- [[deep-research]] - Comprehensive research workflow
- [[paper-discover]] - Find academic papers
- [[slide-maker]] - Create presentations
- [[vault-graph]] - Analyze wikilinks as a graph
- [[recall]] - Memory-based learning

## Updating Skills

```bash
cd /mnt/data/ai-skills/superpowers && git pull
cd /mnt/data/ai-skills/obsidian-skills && git pull
cd /mnt/data/ai-skills/obsidian-vault-agent && git pull
```

## Source Repositories

- [[obra/superpowers]] - https://github.com/obra/superpowers
- [[kepano/obsidian-skills]] - https://github.com/kepano/obsidian-skills
- [[tuan3w/obsidian-vault-agent]] - https://github.com/tuan3w/obsidian-vault-agent

## Related

- [[AI CLI Tools Setup]]
- [[Obsidian Knowledge Management]]
- [[Software Development Workflow]]

---

*Installed with [[OpenCode]] on 2026-04-16*
