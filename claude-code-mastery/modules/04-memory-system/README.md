# Module 04: Memory & Project Intelligence

**Claude Code Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Module Overview

Memory is what transforms Claude Code from a **generic AI assistant** into a **project-aware teammate**. This module teaches you how Claude Code remembers your preferences, project conventions, and team standards across sessions — and how you control every aspect of that system.

Without memory, every new session starts from zero. With a well-configured memory system, Claude Code already knows your build commands, coding style, architecture decisions, and team rules before you type a single prompt.

---

## Learning Objectives

- Understand the full CLAUDE.md file hierarchy and load order
- Configure project-level, user-level, and enterprise-level memory
- Use the auto-memory system for hands-free learning
- Create path-scoped rules with `.claude/rules/`
- Apply best practices to keep memory files effective and maintainable

---

## Lessons

| Lesson | Topic | Description |
|--------|-------|-------------|
| 1 | [Module Overview](README.md) | This page |
| 2 | [CLAUDE.md Files](claude-md-files.md) | Complete guide to all CLAUDE.md locations and loading |
| 3 | [Auto-Memory System](auto-memory.md) | Automatic memory creation and management |
| 4 | [Rules Directory](rules-directory.md) | `.claude/rules/` for path-scoped instructions |
| 5 | [Best Practices](best-practices.md) | Keeping your memory system clean and effective |

---

## Key Concepts at a Glance

| Concept | Purpose | Scope |
|---------|---------|-------|
| `CLAUDE.md` | Project instructions and conventions | Project / User / Enterprise |
| Auto-memory | Claude learns and remembers on its own | Per-project, stored in `~/.claude/` |
| `.claude/rules/` | Path-scoped and topic-specific rules | Project-level, checked into git |
| `@import` syntax | Split large instructions into files | Any CLAUDE.md file |

---

## How Memory Flows into a Session

```
┌─────────────────────────────────────────────────┐
│                  SESSION START                    │
├─────────────────────────────────────────────────┤
│  1. Managed policy    /etc/claude-code/CLAUDE.md │
│  2. Parent dirs       ../CLAUDE.md (walks up)    │
│  3. Project root      ./CLAUDE.md                │
│  4. User-level        ~/.claude/CLAUDE.md        │
│  5. Auto-memory       ~/.claude/projects/.../    │
│  6. Rules directory   .claude/rules/*.md         │
├─────────────────────────────────────────────────┤
│  7. Subdirectory      src/api/CLAUDE.md (lazy)   │
└─────────────────────────────────────────────────┘
```

Higher-numbered sources can be overridden by lower-numbered ones. Managed policy always wins.

---

## Prerequisites

- Completed Module 03 (Core Commands)
- A project directory with at least a few files
- Claude Code installed and authenticated

---

**Start:** [CLAUDE.md Files →](claude-md-files.md)

[← Previous Module](../03-core-commands/) | [Course Home](../../README.md) | [Next Module →](../05-tools-and-workflows/)

---

*Module 04 — Claude Code Mastery — March 2026*
