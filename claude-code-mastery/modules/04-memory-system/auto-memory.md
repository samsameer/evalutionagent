# Auto-Memory System

**Module 04, Lesson 3 — Claude Code Mastery**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Auto-memory is Claude Code's ability to **learn and remember things on its own** without you manually editing CLAUDE.md files. When enabled, Claude detects important patterns, preferences, and corrections during your conversations and saves them for future sessions.

Think of it as Claude taking notes for itself. You correct a behavior once, and Claude remembers it forever.

---

## How Auto-Memory Works

During a conversation, Claude may recognize information worth remembering:

- You correct a coding style preference
- You explain a project convention
- You clarify how a build system works
- You describe an architectural decision

Claude saves this to a **memory file** in your local filesystem. The next time you start a session in the same project, Claude reads these files and already knows what you taught it.

```
You: "Don't use console.log for debugging — use our custom logger from src/utils/logger.ts"

Claude: *saves to memory*
  → Remembered: Use custom logger (src/utils/logger.ts) instead of console.log
```

---

## Storage Location

Auto-memory files are stored at:

```
~/.claude/projects/<project-hash>/memory/
```

The `<project-hash>` is derived from the absolute path to your project directory. This means:

| Scenario | Memory Sharing |
|----------|---------------|
| Same project, same machine | Shared |
| Same project, different terminal | Shared |
| Same project, different git branch | Shared |
| Same project, different worktree | Shared |
| Different project | Separate |
| Same project, different machine | Not shared (local only) |

> **Important:** All git worktrees of the same repository share one memory directory. Memory is tied to the project, not the branch.

---

## MEMORY.md — The Primary Memory File

The main auto-memory file is `MEMORY.md` inside the memory directory:

```
~/.claude/projects/<project-hash>/memory/MEMORY.md
```

### Loading Behavior

| Lines | Behavior |
|-------|----------|
| Lines 1–200 | Loaded automatically at session start |
| Lines 201+ | Lazy-loaded when Claude needs them |

This means the **first 200 lines** of MEMORY.md are always in Claude's context. Content beyond line 200 is still available but only loaded on demand to save context window space.

### What Gets Stored

Claude automatically saves things like:

```markdown
## Project Preferences
- Use pnpm, not npm
- Run tests with: pnpm test --reporter=verbose
- Prefer Zod for runtime validation over io-ts

## Code Style Corrections
- Always destructure props in React components
- Use `type` instead of `interface` for non-extendable types
- Error messages should be user-facing (no technical jargon)

## Architecture Notes
- src/services/ contains business logic — never import Express here
- All database access goes through src/db/repositories/
- Feature flags are managed via LaunchDarkly SDK
```

---

## Topic-Specific Memory Files

Beyond MEMORY.md, Claude can create **topic-specific files** in the memory directory:

```
~/.claude/projects/<project-hash>/memory/
├── MEMORY.md              # General project memory
├── testing-patterns.md    # How tests are structured
├── api-conventions.md     # API design decisions
└── deployment-notes.md    # Deployment-specific knowledge
```

Claude creates these when a topic grows large enough to warrant its own file. Topic-specific files are lazy-loaded — they are read when Claude encounters a related task.

---

## Enabling and Disabling Auto-Memory

### Toggle via /memory Command

```
/memory
```

The `/memory` interface shows the current auto-memory status and lets you toggle it on or off.

### Toggle via Settings

```
/config
```

Navigate to the auto-memory setting, or set it directly in your configuration:

```json
{
  "autoMemoryEnabled": true
}
```

### Configuration Locations

| Method | Scope |
|--------|-------|
| `/memory` toggle | Current session + future sessions |
| `/config` setting | Persistent across all sessions |
| `autoMemoryEnabled` in settings.json | Persistent across all sessions |

---

## What Auto-Memory Captures vs. Ignores

### Good Candidates for Auto-Memory

- Coding style preferences you correct repeatedly
- Project-specific build or test commands
- Architecture decisions explained during conversation
- Tool preferences (formatter, linter, package manager)
- Common patterns specific to the project

### Not Stored in Auto-Memory

- Sensitive data (API keys, passwords, credentials)
- One-time instructions ("just this once, use tabs")
- Transient debugging context
- File contents (Claude re-reads files as needed)

---

## Managing Auto-Memory

### Viewing Memory Files

Use `/memory` to browse all loaded memory files. You can also inspect them directly:

```bash
# Find your project's memory directory
ls ~/.claude/projects/

# Read the memory file
cat ~/.claude/projects/<project-hash>/memory/MEMORY.md
```

### Editing Memory Files

You can edit memory files directly with any text editor. Changes take effect on the next session (or after `/clear`).

```bash
# Open in your editor
code ~/.claude/projects/<project-hash>/memory/MEMORY.md
```

### Clearing Memory

To reset auto-memory for a project:

```bash
# Remove all memory files
rm -rf ~/.claude/projects/<project-hash>/memory/
```

Claude will start learning again from scratch in the next session.

---

## Auto-Memory vs. CLAUDE.md

| Feature | CLAUDE.md | Auto-Memory |
|---------|-----------|-------------|
| Who writes it | You (manually) | Claude (automatically) |
| Shared with team | Yes (committed to git) | No (local to your machine) |
| Location | Project directory | `~/.claude/projects/` |
| Best for | Team conventions, build commands | Personal corrections, learned preferences |
| Load behavior | Always loaded at start | First 200 lines at start, rest lazy |
| Editable | Yes | Yes (but Claude may update it) |

**Rule of thumb:** If the whole team needs to know it, put it in CLAUDE.md. If it is personal or Claude learned it from your corrections, let auto-memory handle it.

---

## Tips for Effective Auto-Memory

- **Let Claude learn naturally.** Correct it once clearly, and it remembers.
- **Review memory periodically.** Run `/memory` to see what Claude has saved and remove outdated entries.
- **Keep MEMORY.md under 200 lines.** Content beyond 200 lines is lazy-loaded and may not be immediately available.
- **Do not duplicate CLAUDE.md content.** If something is in CLAUDE.md, Claude does not need to also save it in auto-memory.
- **Trust the system.** Auto-memory is designed to capture what matters without intervention.

---

**Next:** [Rules Directory](rules-directory.md)

[← Back to Module Overview](README.md)

---

*Module 04, Lesson 3 — Claude Code Mastery — March 2026*
