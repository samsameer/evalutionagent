# Memory Best Practices

**Module 04, Lesson 5 — Claude Code Mastery**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

A well-maintained memory system makes Claude Code dramatically more effective. A poorly maintained one wastes context window space, creates conflicting instructions, and confuses Claude. This lesson covers the practices that separate effective memory configurations from messy ones.

---

## Keep Files Under 200 Lines

The first 200 lines of any memory file are loaded eagerly. Content beyond that threshold is lazy-loaded and may not be immediately available. Keeping files concise ensures Claude always has your most important instructions.

| File Size | Effect |
|-----------|--------|
| Under 100 lines | Ideal — fully loaded, leaves context for your work |
| 100–200 lines | Good — fully loaded at start |
| 200–500 lines | Risky — content after line 200 is lazy-loaded |
| 500+ lines | Too large — split into multiple files with imports |

---

## Use Markdown Headers and Bullets

Claude parses CLAUDE.md as Markdown. Structure matters. Well-formatted files are parsed more reliably than walls of text.

**Bad — unstructured paragraph:**
```markdown
When writing code for this project you should use TypeScript and make sure
to use strict mode and also use ESLint and Prettier and run tests with
vitest and the coverage should be above 80% and also use pnpm not npm
and make sure to follow the existing patterns in the codebase.
```

**Good — structured with headers and bullets:**
```markdown
## Build Tools
- Package manager: pnpm (not npm)
- Test runner: Vitest
- Linter: ESLint with strict config
- Formatter: Prettier

## Code Standards
- Language: TypeScript in strict mode
- Coverage target: 80% minimum for new code
- Follow existing patterns in the codebase
```

---

## Be Specific — Good vs. Bad Examples

Vague instructions lead to inconsistent behavior. Specific instructions produce reliable results.

| Bad (Vague) | Good (Specific) |
|-------------|-----------------|
| "Write good tests" | "Use Vitest with `describe`/`it` blocks. Mock HTTP calls with msw. Assert both success and error paths." |
| "Follow best practices" | "Use early returns. Limit functions to 30 lines. No nested ternaries." |
| "Use proper error handling" | "Wrap async operations in try/catch. Use `AppError` class from `src/errors.ts`. Log with `logger.error()`." |
| "Keep code clean" | "Run `pnpm lint` before committing. No unused imports. No `any` types." |
| "Use the right patterns" | "Use repository pattern for database access. Use Result<T, E> for operations that can fail." |

---

## Split Large Files with Imports

When a CLAUDE.md file grows beyond 200 lines, split it using `@import` syntax:

**Before — one massive file (400+ lines):**
```markdown
# Project Instructions

## Build commands
... (50 lines)

## Code style
... (80 lines)

## API conventions
... (100 lines)

## Testing guide
... (90 lines)

## Deployment
... (80 lines)
```

**After — modular with imports:**
```markdown
# Project Instructions

@docs/build-commands.md
@docs/code-style.md
@docs/api-conventions.md
@docs/testing-guide.md
@docs/deployment.md
```

Each imported file stays focused and under the 200-line threshold.

---

## Review Periodically for Conflicts

Memory files can accumulate contradictory instructions over time, especially when multiple team members contribute:

**Conflict example:**
```markdown
# CLAUDE.md (project root)
- Use interfaces for all type definitions

# .claude/rules/code-style.md
- Use type aliases instead of interfaces for non-extendable types
```

Schedule periodic reviews:
- Check for contradictions between CLAUDE.md and rules files
- Remove instructions for deprecated tools or patterns
- Update build commands after dependency upgrades
- Verify that path-scoped rules still match the current directory structure

---

## What Survives /compact

When you run `/compact`, Claude summarizes the conversation to free context space. Understanding what survives compaction helps you decide where to put instructions.

| Survives /compact | Does NOT Survive /compact |
|-------------------|--------------------------|
| CLAUDE.md files (re-read from disk) | Verbal instructions in early conversation |
| .claude/rules/ files | Detailed tool output from earlier turns |
| Auto-memory files | Specific examples you described verbally |
| Key decisions and outcomes | Long code snippets shown in conversation |
| Recent conversation turns | Context from old debugging sessions |

**Takeaway:** If an instruction is important enough to survive compaction, it belongs in a file (CLAUDE.md, rules, or auto-memory) — not in the conversation.

---

## What to Put in CLAUDE.md vs. Conversation

Not everything belongs in CLAUDE.md. Some instructions are better given in the conversation.

| Put in CLAUDE.md | Say in Conversation |
|------------------|---------------------|
| Build commands | "Run the build and check for errors" |
| Code style rules | "In this specific case, skip the lint check" |
| Architecture patterns | "Refactor this function to use the new pattern" |
| Team conventions | "Just this once, use a quick workaround" |
| Testing requirements | "Focus on testing the edge case for null input" |
| Permanent preferences | Temporary overrides for one task |

**Rule of thumb:** If you would tell every new team member, it goes in CLAUDE.md. If it is specific to this moment, say it in conversation.

---

## Compact Instructions Section

Add a dedicated section to your CLAUDE.md that tells Claude how to behave during and after compaction:

```markdown
## Compact Instructions

When compacting this conversation:
- Always preserve the current task objective and acceptance criteria
- Keep track of which files have been modified and why
- Retain any failing test names and error messages
- Summarize architectural decisions made during this session
- Drop verbose command output and intermediate debugging steps
```

This ensures that when `/compact` runs, Claude prioritizes the right information in its summary.

---

## Memory System Checklist

Use this checklist when setting up a new project:

- [ ] Run `/init` to generate an initial CLAUDE.md
- [ ] Review and edit the generated CLAUDE.md for accuracy
- [ ] Add build, test, and lint commands
- [ ] Add code style rules with specific examples
- [ ] Create `.claude/rules/` files for detailed topic areas
- [ ] Add `paths` frontmatter to rules that only apply to certain directories
- [ ] Enable auto-memory (`/memory` toggle or `/config`)
- [ ] Add a compact instructions section
- [ ] Commit CLAUDE.md and `.claude/rules/` to git
- [ ] Share with team and gather feedback

---

## Common Mistakes to Avoid

| Mistake | Why It Hurts | Fix |
|---------|-------------|-----|
| 500-line CLAUDE.md | Most content lazy-loaded; wastes context | Split with `@import` or use rules files |
| Contradictory rules across files | Claude gets confused, follows neither | Review and reconcile regularly |
| Too vague ("write good code") | No actionable guidance | Be specific with examples |
| Duplicating rules in multiple places | Updates missed in some copies | Single source of truth; use imports |
| Putting secrets in CLAUDE.md | Committed to git, visible to team | Use `.env` files and reference them |
| Never reviewing memory | Stale instructions cause wrong behavior | Review monthly or after major changes |
| Relying only on conversation | Instructions lost on `/compact` or `/clear` | Save persistent rules to files |

---

## Summary

The memory system is most effective when you treat it like code: keep it organized, review it regularly, and make it specific. A focused 50-line CLAUDE.md with a few targeted rules files will outperform a 500-line monolith every time.

---

**Done with Module 04!**

[← Back to Module Overview](README.md)

[← Previous Module](../03-core-commands/) | [Course Home](../../README.md) | [Next Module →](../05-tools-and-workflows/)

---

*Module 04, Lesson 5 — Claude Code Mastery — March 2026*
