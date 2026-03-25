# CLAUDE.md Files — The Complete Guide

**Module 04, Lesson 2 — Claude Code Mastery**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

CLAUDE.md files are the primary way you give Claude Code persistent instructions. They work like a combination of a dotfile and a team wiki — loaded automatically at the start of every session so Claude already knows your project's conventions, build commands, and coding standards.

Claude Code reads CLAUDE.md files from **multiple locations**, each serving a different purpose. Understanding where to place instructions and how the load order works is the key to a well-configured project.

---

## All CLAUDE.md Locations

| Location | Purpose | Shared with Team? | Loaded |
|----------|---------|-------------------|--------|
| `/etc/claude-code/CLAUDE.md` | Enterprise managed policy | N/A (admin-set) | Always first |
| `../CLAUDE.md` (parent dirs) | Monorepo / workspace rules | Yes (if committed) | Walks up to root |
| `./CLAUDE.md` or `./.claude/CLAUDE.md` | Project-level instructions | Yes (committed to git) | At session start |
| `~/.claude/CLAUDE.md` | User-level personal prefs | No (local only) | At session start |
| `.claude/CLAUDE.md` (gitignored) | Local project overrides | No (gitignored) | At session start |
| `src/api/CLAUDE.md` (subdirectory) | Directory-specific rules | Yes (committed) | Lazy-loaded on access |

---

## Project-Level CLAUDE.md

The most common location. Place it at the root of your project:

```
myproject/
├── CLAUDE.md              # Option A: root level
├── .claude/
│   └── CLAUDE.md          # Option B: inside .claude/
├── src/
└── package.json
```

Both locations are equivalent. If both exist, both are loaded. This file should contain:

- Build and test commands
- Code style rules
- Architecture decisions
- Common patterns used in the project

```markdown
# Project Instructions

## Build Commands
- `npm run build` — Production build
- `npm test` — Run test suite
- `npm run lint` — Run ESLint

## Code Style
- Use TypeScript strict mode
- Prefer named exports over default exports
- All API handlers must use the Result<T, E> pattern
- Never use `any` type — use `unknown` and narrow

## Architecture
- src/api/ — Express route handlers
- src/services/ — Business logic (no HTTP concerns)
- src/db/ — Database queries using Drizzle ORM
```

---

## User-Level CLAUDE.md

Located at `~/.claude/CLAUDE.md`, this file applies to **every project** you work on. Use it for personal preferences that are not project-specific:

```markdown
# Personal Preferences

- I prefer concise code comments over verbose ones
- Always use early returns instead of nested if/else
- When suggesting terminal commands, use zsh syntax
- I use VS Code — reference its keybindings when relevant
- Prefer functional programming patterns where practical
```

> **Tip:** Keep this file short. Project-specific rules belong in the project CLAUDE.md, not here.

---

## Local .claude/CLAUDE.md (Gitignored)

The `.claude/` directory typically has a `.gitignore` entry for `CLAUDE.md`, allowing you to keep local overrides that are not shared with the team:

```markdown
# Local Overrides (not committed)

- My local database is on port 5433, not 5432
- Use `pnpm` instead of `npm` (my local setup)
- Skip integration tests: run `npm test -- --grep "unit"` only
```

This is useful for environment-specific differences that should not affect teammates.

---

## Managed Policy CLAUDE.md (Enterprise)

Enterprise administrators can place a policy file at:

| Platform | Path |
|----------|------|
| Linux | `/etc/claude-code/CLAUDE.md` |
| macOS | `/etc/claude-code/CLAUDE.md` |

This file is loaded **first** and has the **highest priority**. It cannot be overridden by project or user files. Typical enterprise uses:

- Security policies ("Never commit secrets or API keys")
- Compliance requirements ("All database changes require migration files")
- Approved libraries and patterns
- Forbidden operations

---

## Parent Directory CLAUDE.md Files

Claude Code walks **up the directory tree** from your project root, loading any CLAUDE.md files it finds. This is especially useful in monorepos:

```
workspace/
├── CLAUDE.md              # Workspace-wide rules (loaded)
├── packages/
│   ├── CLAUDE.md          # Shared package rules (loaded)
│   ├── frontend/
│   │   ├── CLAUDE.md      # Frontend rules (project root)
│   │   └── src/
│   └── backend/
│       ├── CLAUDE.md      # Backend rules (project root)
│       └── src/
```

If you run Claude Code from `workspace/packages/frontend/`, it loads:
1. `workspace/CLAUDE.md`
2. `workspace/packages/CLAUDE.md`
3. `workspace/packages/frontend/CLAUDE.md`

---

## Subdirectory Lazy-Loading

CLAUDE.md files in subdirectories are **not loaded at session start**. They are loaded **on demand** when Claude reads or edits files in that directory:

```
myproject/
├── CLAUDE.md                  # Loaded at start
├── src/
│   ├── api/
│   │   └── CLAUDE.md          # Loaded when Claude touches src/api/
│   └── components/
│       └── CLAUDE.md          # Loaded when Claude touches src/components/
```

Use subdirectory CLAUDE.md files for directory-specific conventions:

```markdown
# API Route Conventions

- Every route handler must validate input with Zod schemas
- Always return consistent error shapes: { error: string, code: number }
- Log all 5xx errors with request ID
```

---

## Import Syntax: @path/to/file

Split large CLAUDE.md files using the `@import` syntax:

```markdown
# Project Instructions

@docs/coding-standards.md
@docs/api-conventions.md
@docs/testing-guide.md
```

Each `@path` line imports the contents of that file relative to the CLAUDE.md location. This keeps individual files small and focused.

**Rules for imports:**
- One `@path` per line
- Paths are relative to the CLAUDE.md file's directory
- Imported files can themselves contain `@imports` (nested)
- Non-existent files are silently skipped

---

## Load Order and Priority

When instructions conflict, this is the priority order (highest to lowest):

| Priority | Source | Can Override? |
|----------|--------|---------------|
| 1 (highest) | Managed policy (`/etc/claude-code/CLAUDE.md`) | No — always wins |
| 2 | Parent directory CLAUDE.md files | By priority 1 only |
| 3 | Project root CLAUDE.md | By 1 and 2 |
| 4 | User-level (`~/.claude/CLAUDE.md`) | By 1, 2, and 3 |
| 5 | Local `.claude/CLAUDE.md` (gitignored) | By 1, 2, and 3 |
| 6 (lowest) | Subdirectory CLAUDE.md (lazy-loaded) | By all above |

> **Key insight:** Managed policy always wins. Project-level rules override personal preferences. Subdirectory rules are additive context, not overrides.

---

## The /memory Command

Use `/memory` in a Claude Code session to browse all currently loaded memory:

```
/memory
```

This shows:
- Every CLAUDE.md file currently loaded and its source path
- Rules from `.claude/rules/` directory
- Auto-memory files and their status
- Toggle auto-memory on or off

You can open any listed file directly in your editor from the `/memory` interface.

---

## The /init Command

Run `/init` to have Claude analyze your project and generate a CLAUDE.md:

```
/init
```

Claude will:
1. Scan your project structure and files
2. Identify the language, framework, and build system
3. Discover test commands and linting configuration
4. Detect coding patterns and conventions
5. Generate a CLAUDE.md tailored to your project

If a CLAUDE.md already exists, `/init` reviews it and suggests additions or improvements rather than overwriting.

---

**Next:** [Auto-Memory System](auto-memory.md)

[← Back to Module Overview](README.md)

---

*Module 04, Lesson 2 — Claude Code Mastery — March 2026*
