---
title: AI CLI Skills Installation
date: 2026-04-16
updated: 2026-05-03
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

Installed **49 skills** across four collections:

| Collection | Count | Purpose |
|------------|-------|---------|
| [[Superpowers]] | 13 | Development workflow |
| [[Obsidian Skills]] | 5 | Vault management |
| [[Obsidian Vault Agent]] | 12 | AI knowledge management |
| [[Design Skills]] | 19 | UI/UX and web design |

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

## Design Skills

Premium UI/UX and web design skills from top designers (installed 2026-05-03):

### Premium Design Engines
- [[emil-design-eng]] - Emil Kowalski's design engineering philosophy (animations, component design, UI polish)
- [[impeccable]] - Paul Bakaus's design language with 23 commands (craft, audit, critique, polish, animate, etc.)
- [[taste-skill]] - Anti-slop frontend with 3-dial system (DESIGN_VARIANCE, MOTION_INTENSITY, VISUAL_DENSITY)

### Taste Skill Variants
- [[soft-skill]] - Luxury aesthetic with ethereal glass and spring animations
- [[minimalist-skill]] - Clean Notion/Linear-inspired editorial UI
- [[brutalist-skill]] - Swiss typography meets terminal aesthetics (β)
- [[redesign-skill]] - Audit and upgrade existing projects
- [[output-skill]] - Anti-laziness enforcement (no placeholder code)
- [[stitch-skill]] - Google Stitch-compatible design rules
- [[gpt-tasteskill]] - Stricter variant for GPT/Codex models

### Design Intelligence
- [[ui-ux-pro-max]] - Design system generator (161 product types, 161 color palettes, 57 font pairings)
- [[design-auditor]] - 18-category design audit with severity ratings
- [[web-design-studio]] - Production-grade design with auto-generated images and documentation

### Additional Symlinks for IDEs
Additional IDEs with separate skills folders also have symlinks to central location:
- [[openclaw]]: ~/.openclaw/skills/
- [[cursor]]: ~/.cursor/skills-cursor/
- [[trae]]: ~/.trae/skills/
- [[qoder]]: ~/.qoder/skills/
- [[continue]]: ~/.continue/skills/
- [[factory]]: ~/.factory/skills/
- [[kiro]]: ~/.kiro/skills/

## Updating Skills

```bash
cd /mnt/data/ai-skills/superpowers && git pull
cd /mnt/data/ai-skills/obsidian-skills && git pull
cd /mnt/data/ai-skills/obsidian-vault-agent && git pull
```

## Source Repositories

### Development Skills
- [[obra/superpowers]] - https://github.com/obra/superpowers
- [[kepano/obsidian-skills]] - https://github.com/kepano/obsidian-skills
- [[tuan3w/obsidian-vault-agent]] - https://github.com/tuan3w/obsidian-vault-agent

### Design Skills
- [[emilkowalski/skill]] - https://github.com/emilkowalski/skill
- [[pbakaus/impeccable]] - https://github.com/pbakaus/impeccable
- [[Leonxlnx/taste-skill]] - https://github.com/Leonxlnx/taste-skill
- [[nextlevelbuilder/ui-ux-pro-max-skill]] - https://github.com/nextlevelbuilder/ui-ux-pro-max-skill
- [[Ashutos1997/claude-design-auditor-skill]] - https://github.com/Ashutos1997/claude-design-auditor-skill
- [[xiaodong-wu/web-design-studio]] - https://github.com/xiaodong-wu/web-design-studio

## Related

- [[AI CLI Tools Setup]]
- [[Obsidian Knowledge Management]]
- [[Software Development Workflow]]
- [[Web Design Skills 2026]]

---

*Installed with [[OpenCode]] on 2026-04-16, updated 2026-05-03 with design skills*
