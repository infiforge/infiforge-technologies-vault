---
name: Infiforge Vault
description: Infiforge services knowledge base - all work from ~/work folder recorded here
---

# Infiforge Vault Rules

This vault is my second brain connected to OpenCode for ALL Infiforge work in ~/work folder.

## CRITICAL: Work Folder Memory Rule

**EVERY change in ~/work folder MUST be recorded in this vault:**

| Work Location | Vault Location | Note Type |
|---------------|----------------|-----------|
| `~/work/services/internal/[name]/` | `Projects/[Name] — [Type].md` | Project note |
| `~/work/libraries/deno/[name]/` | `Memory/[Name] Library.md` | Library documentation |
| `~/work/libraries/flutter/[name]/` | `Memory/[Name] Library.md` | Library documentation |
| `~/work/tools/` | `Memory/[Tool Name].md` | Tool documentation |
| `~/work/services/external/[name]/` | `Projects/[Name] — External Service.md` | External service |

## Automatic Memory Capture

**ALWAYS automatically save WITHOUT asking:**

1. **New service created** → `Projects/[Service Name] — [Type].md`
2. **New library created** → `Memory/[Library Name] Library.md`
3. **Library updated/changed** → Update existing `Memory/[Library Name] Library.md`
4. **Service architecture change** → Update existing project note
5. **Tech stack decision** → `Decisions/YYYY-MM-DD — [topic].md`
6. **Every session involving work** → `Journal/YYYY-MM-DD.md`

## Library Documentation Structure

For Deno and Flutter libraries, document in `Memory/[Name] Library.md`:

```yaml
---
date: 2026-04-11
updated: 2026-04-11
tags:
  - library
  - deno  # or flutter
  - [library-name]
---

# [Library Name] Library

## Overview
Brief description of what the library does

## Exports
List key exports and their purposes

## Usage Pattern
Code examples showing how to use

## Dependencies
What other libraries it depends on

## Recent Updates
Keep track of changes with dates
```

## Service Project Structure

For services in `services/internal/`, use:

```yaml
---
date: 2026-04-11
tags:
  - project
  - service
---

# [Service Name] - [Description]

## Service Details
| Attribute | Value |
|-----------|-------|
| **Name** | [Name] |
| **Type** | Backend/Frontend/Full-stack |
| **Location** | `services/internal/[name]/` |
| **Port Range** | XXXX-XXXX |

## Technology Stack
- Backend: [tech]
- Frontend: [tech]

## Libraries Used
List all libraries used

## Key Patterns
Architecture patterns used

## Status
active/planning/on-hold
```

## Daily Workflow

1. Start with checking relevant project/library notes if working on existing
2. Make changes in ~/work folder
3. IMMEDIATELY update vault with any changes
4. End sessions by updating Journal

## Key Principles

- Save everything worth remembering (when in doubt, save it)
- Link related notes with [[wikilinks]]
- Use frontmatter for metadata (date, tags, updated)
- NEVER ask "should I save this?" - just save it
- Update existing notes when making changes (don't create new)
- Use "updated:" frontmatter field to track changes

## Vault Structure

```
Infiforge Vault/
├── Projects/           # All services in ~/work/services/internal/
│   ├── [Name] — [Type].md
│   └── ... (10 services)
├── Memory/             # All libraries in ~/work/libraries/
│   ├── [Name] Library.md (Deno + Flutter)
│   └── 2026-04-11 — Tech Stack Overview.md
├── Decisions/          # Architecture decisions
├── Journal/            # Session logs
├── People/             # Contact notes
└── Areas/              # Areas of focus
```

## Library Documentation

Libraries are documented in `Memory/[Name] Library.md`:
- Deno libraries: `libraries/deno/[name]/`
- Flutter libraries: `libraries/flutter/[name]/`

The master library overview is `Memory/2026-04-11 — Tech Stack Overview.md`

## Service Project Notes

Services are documented in `Projects/[Name] — [Type].md`:
- Internal services: `services/internal/[name]/`
- External services: `services/external/[name]/`

## Systematic Vault Update Process

To keep the vault current with all work in ~/work folder:

### Daily
- End-of-day journal entry in `Journal/YYYY-MM-DD.md` documenting what was done
- Use git commit messages as source for journal entries

### Per Change
- Update relevant project/library note immediately when making changes
- For service changes: update `Projects/[Name] — [Type].md`
- For library changes: update `Memory/[Name] Library.md`
- For architecture decisions: create `Decisions/YYYY-MM-DD — [topic].md`

### Per Decision
- Create decision note in `Decisions/` BEFORE implementing
- Use [[Templates/Decision Note Template.md]] for consistency

### Weekly
- Review vault for outdated notes
- Check that all recent work is documented
- Update "updated:" frontmatter fields

### Per Workplan Phase
- Update vault when workplan phase completes
- Document completion in Journal
- Update relevant project notes with new status

### Automation
- Add vault update step to workplan.md phases
- Use [[Templates/Daily Journal Template.md]] for daily entries
- Use [[Templates/Project Note Template.md]] for new services
- Use [[Templates/Library Note Template.md]] for new libraries

### Templates Available

- [[Templates/Project Note Template.md]] - For new service notes
- [[Templates/Library Note Template.md]] - For new library documentation
- [[Templates/Decision Note Template.md]] - For architectural decisions
- [[Templates/Daily Journal Template.md]] - For daily session logs
- [[Templates/Service Note Template.md]] - For service-specific notes (AGENTS.md, etc.)

### Areas

For organizing related work:
- [[Areas/Backend Development]] - Backend services and Deno libraries
- [[Areas/Frontend Development]] - Flutter frontends and libraries
- [[Areas/Infrastructure]] - Deployment, monitoring, CI/CD
- [[Areas/Architecture]] - Architectural decisions and patterns
- [[Areas/DevOps]] - DevOps practices and automation