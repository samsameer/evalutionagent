# The .claude/rules/ Directory

**Module 04, Lesson 4 — Claude Code Mastery**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

The `.claude/rules/` directory lets you create **topic-specific, file-scoped instruction files** that Claude loads automatically. Unlike a single CLAUDE.md that covers everything, rules files let you organize instructions by topic and optionally limit them to specific file paths.

Rules files are committed to git, making them a team-shared resource — like a linter configuration, but for AI behavior.

---

## Directory Structure

Place your rules files inside `.claude/rules/` at the root of your project:

```
myproject/
├── .claude/
│   └── rules/
│       ├── code-style.md
│       ├── testing.md
│       ├── api-design.md
│       ├── security.md
│       └── frontend/
│           ├── react-patterns.md
│           └── css-conventions.md
├── src/
└── package.json
```

Every `.md` file in `.claude/rules/` (including nested subdirectories) is automatically discovered and loaded.

---

## Basic Rules Files

A rules file is a plain Markdown file with instructions for Claude:

**`.claude/rules/code-style.md`**
```markdown
# Code Style Rules

- Use 2-space indentation for TypeScript and JavaScript
- Use 4-space indentation for Python
- Prefer `const` over `let`; never use `var`
- Use template literals instead of string concatenation
- Maximum line length: 100 characters
- Use trailing commas in multiline arrays and objects
```

**`.claude/rules/testing.md`**
```markdown
# Testing Conventions

- Use Vitest for all unit and integration tests
- Test files live next to source: `Button.tsx` → `Button.test.tsx`
- Use `describe` blocks grouped by method or behavior
- Prefer `it("should ...")` naming convention
- Mock external services; never make real HTTP calls in tests
- Minimum coverage target: 80% for new code
```

---

## Path-Scoped Rules with YAML Frontmatter

The most powerful feature of rules files is **path scoping**. Add YAML frontmatter with a `paths` field to limit when a rule is loaded:

**`.claude/rules/api-validation.md`**
```markdown
---
paths:
  - "src/api/**/*.ts"
---

# API Validation Rules

- Every route handler must validate request body with a Zod schema
- Use `z.object()` for request bodies, `z.string().uuid()` for ID params
- Return 400 with validation error details on invalid input
- Never trust client-side validation alone
```

This rule is **only loaded** when Claude reads or edits files matching `src/api/**/*.ts`. It stays out of context otherwise, saving context window space.

### Path Pattern Syntax

Paths use glob patterns:

| Pattern | Matches |
|---------|---------|
| `src/api/**/*.ts` | All TypeScript files under src/api/ |
| `*.test.ts` | All test files in any directory |
| `src/components/**` | All files under src/components/ |
| `migrations/*.sql` | SQL files in migrations/ directory |
| `**/*.css` | All CSS files anywhere in the project |
| `src/db/**/*.ts` | All TypeScript files under src/db/ |

### Multiple Paths

A single rule can apply to multiple path patterns:

```markdown
---
paths:
  - "src/api/**/*.ts"
  - "src/routes/**/*.ts"
  - "src/middleware/**/*.ts"
---

# HTTP Layer Rules

- Always use async/await, never raw Promises
- Catch all errors with the global error handler
- Log request duration for endpoints over 500ms
```

---

## Nested Directories

You can organize rules into subdirectories for large projects:

```
.claude/rules/
├── general/
│   ├── code-style.md
│   └── git-conventions.md
├── backend/
│   ├── api-design.md
│   ├── database.md
│   └── error-handling.md
├── frontend/
│   ├── react-patterns.md
│   ├── accessibility.md
│   └── state-management.md
└── devops/
    ├── docker.md
    └── ci-cd.md
```

All files are discovered recursively. The subdirectory structure is purely for your organizational benefit — it does not affect loading behavior (unless the files use `paths` frontmatter).

---

## Rules vs. CLAUDE.md — When to Use Each

| Use Case | CLAUDE.md | .claude/rules/ |
|----------|-----------|----------------|
| Build and test commands | Yes | No |
| General project description | Yes | No |
| Topic-specific coding standards | Possible, but grows large | Yes — one file per topic |
| Path-scoped instructions | No (always loaded) | Yes — via `paths` frontmatter |
| Quick one-line reminders | Yes | Overkill |
| Detailed multi-paragraph rules | Gets unwieldy | Yes — dedicated file |

**Rule of thumb:** If the instruction is short and universal, put it in CLAUDE.md. If it is a detailed topic or only applies to certain files, create a rules file.

---

## Examples of Effective Rules Files

### Security Rules (Always Loaded)

**`.claude/rules/security.md`**
```markdown
# Security Rules

- Never log sensitive data (passwords, tokens, PII)
- Always parameterize SQL queries — no string interpolation
- Validate and sanitize all user input
- Use bcrypt with cost factor 12 for password hashing
- Set secure, httpOnly, sameSite flags on all cookies
- Never expose stack traces in production error responses
```

### Database Rules (Path-Scoped)

**`.claude/rules/database.md`**
```markdown
---
paths:
  - "src/db/**/*.ts"
  - "migrations/**/*.sql"
---

# Database Conventions

- Use Drizzle ORM for all queries
- Always use transactions for multi-table writes
- Name migrations: YYYYMMDD_HHMMSS_description.sql
- Add indexes for any column used in WHERE clauses
- Use soft deletes (deleted_at timestamp) for user-facing entities
```

### React Component Rules (Path-Scoped)

**`.claude/rules/react-components.md`**
```markdown
---
paths:
  - "src/components/**/*.tsx"
  - "src/pages/**/*.tsx"
---

# React Component Rules

- Use function components with arrow syntax
- Props type goes in the same file, named ComponentNameProps
- Use `React.memo()` only when profiling shows re-render issues
- Prefer composition over prop drilling (use Context or Zustand)
- All interactive elements must have aria-labels
```

---

## Loading Behavior

| Aspect | Behavior |
|--------|----------|
| Discovery | All `.md` files in `.claude/rules/` recursively |
| Non-scoped rules | Loaded at session start (like CLAUDE.md) |
| Path-scoped rules | Loaded when Claude accesses matching files |
| Priority | Same as project-level CLAUDE.md |
| Format | Markdown with optional YAML frontmatter |

---

## Tips

- **Keep each file focused on one topic.** A file covering "everything about testing" is better than one covering "testing, deployment, and logging."
- **Use path scoping for large codebases.** It saves context window space by only loading relevant rules.
- **Commit rules to git.** The whole team benefits from shared AI instructions.
- **Name files descriptively.** `api-error-handling.md` is clearer than `rules3.md`.
- **Review rules when conventions change.** Outdated rules cause Claude to follow old patterns.

---

**Next:** [Best Practices](best-practices.md)

[← Back to Module Overview](README.md)

---

*Module 04, Lesson 4 — Claude Code Mastery — March 2026*
