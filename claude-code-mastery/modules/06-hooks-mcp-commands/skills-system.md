# The Skills System

**Module 06, Lesson 4 --- Claude Code Mastery**

**Instructor: Jabbir Basha, Principal AI Engineer**

---

## What Are Skills?

Skills are on-demand prompt packages that Claude Code loads only when needed. Unlike CLAUDE.md files (which are loaded into every session), skills remain dormant until explicitly invoked. This keeps your context window lean while still giving Claude access to specialized knowledge when a task requires it.

Think of skills as experts that Claude can consult --- they are not in the room at all times, but Claude can call on them when their expertise is relevant.

---

## How Skills Work

```
┌────────────────────┐
│   Claude Session    │
│                     │
│  CLAUDE.md: always  │──────── loaded at startup
│  loaded             │
│                     │
│  Skills: loaded     │──────── loaded on demand when invoked
│  on demand          │
└────────────────────┘
```

| Aspect | Behavior |
|--------|----------|
| Loading | Only when explicitly invoked via the Skill tool or slash command |
| Context cost | Zero until invoked; full prompt loaded when called |
| Persistence | Active for the tool call that invoked them, then released |
| Invocation | `Skill` tool call, `/skill-name` command, or automatic matching |

---

## Built-in Skills

Claude Code ships with several built-in skills for common tasks:

| Skill | Purpose | Invoked By |
|-------|---------|------------|
| `commit` | Create well-structured git commits | `/commit` |
| `review-pr` | Review a pull request | `/review-pr` |
| `pdf` | Read and analyze PDF files | `/pdf` or automatic |
| `ms-office-suite:pdf` | Advanced PDF handling via Office suite | Fully qualified name |

Built-in skills are maintained by Anthropic and updated with Claude Code releases. You can list available skills by checking the system reminders in your session.

---

## Invoking Skills

There are three ways to invoke a skill:

### 1. Slash Command Syntax

Type the skill name as a slash command in the chat:

```
> /commit
> /review-pr 123
> /pdf report.pdf
```

### 2. Skill Tool Call (Programmatic)

Claude itself can invoke skills via the `Skill` tool when it determines one is relevant:

```json
{
  "skill": "review-pr",
  "args": "123"
}
```

### 3. Fully Qualified Name

For skills provided by extensions or MCP servers, use the full namespace:

```
> /ms-office-suite:pdf
```

---

## Creating Custom Skills

Custom skills are Markdown files with optional YAML frontmatter. They follow this structure:

### File Structure

```
.claude/
  skills/
    react-patterns.md
    api-design.md
    database-migrations.md
```

### Skill File Anatomy

```markdown
---
model: claude-opus-4-6
effort: high
disable-model-invocation: false
---

# React Patterns Expert

You are a React architecture expert. When consulted, provide guidance on:

1. Component composition and prop design
2. State management patterns (local state, context, external stores)
3. Performance optimization (memo, useMemo, useCallback, virtualization)
4. Testing strategies for React components
5. Server component vs client component decisions

Always provide concrete code examples alongside explanations.
Reference the project's existing patterns found in src/components/ when suggesting changes.
```

---

## Skill Frontmatter Options

The YAML frontmatter block at the top of a skill file controls its behavior:

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| `model` | `string` | Session default | Override the model used when this skill is active |
| `effort` | `string` | `"medium"` | Reasoning effort level: `"low"`, `"medium"`, or `"high"` |
| `disable-model-invocation` | `boolean` | `false` | If `true`, Claude cannot invoke this skill autonomously --- only the user can trigger it |

### Frontmatter Examples

**Lightweight triage skill (fast, low cost):**

```yaml
---
effort: low
---
```

**High-stakes review skill (maximum reasoning):**

```yaml
---
model: claude-opus-4-6
effort: high
disable-model-invocation: true
---
```

**Default behavior (no frontmatter needed):**

```markdown
# My Skill

Just start writing the prompt. Frontmatter is optional.
```

---

## Skills vs CLAUDE.md

This is one of the most common questions. Here is a direct comparison:

| Dimension | Skills | CLAUDE.md |
|-----------|--------|-----------|
| **Loading** | On demand | Every session, automatically |
| **Context cost** | Zero until invoked | Always consumes tokens |
| **Best for** | Specialized, infrequent tasks | Universal project rules |
| **Scope** | Task-specific expertise | Project-wide standards |
| **Examples** | React migration guide, SQL optimization | Coding style, branch naming, test requirements |
| **Invocation** | Explicit (user or Claude) | Implicit (always present) |
| **Update frequency** | Change anytime, no session impact | Changes affect every session |

### Decision Flowchart

```
Is this knowledge needed in EVERY session?
├── Yes  -->  Put it in CLAUDE.md
└── No
    ├── Is it a multi-step workflow?
    │   └── Yes  -->  Make it a Custom Command
    └── Is it specialized domain knowledge?
        └── Yes  -->  Make it a Skill
```

---

## When to Use Skills vs Memory

The memory system (CLAUDE.md files) and skills serve different purposes:

| Scenario | Use Memory (CLAUDE.md) | Use a Skill |
|----------|----------------------|-------------|
| "Always use TypeScript strict mode" | Yes | No |
| "Our API follows REST conventions" | Yes | No |
| "Guide me through a React 18 to 19 migration" | No | Yes |
| "Optimize slow PostgreSQL queries" | No | Yes |
| "Run tests before committing" | Yes | No |
| "Generate OpenAPI specs from our routes" | No | Yes |
| "Use conventional commit messages" | Yes | No |
| "Analyze bundle size and suggest code splits" | No | Yes |

**Rule of thumb:** If it is a permanent project rule, use CLAUDE.md. If it is expert knowledge for occasional tasks, use a skill.

---

## Practical Example: Building a Skill Library

Here is a set of skills for a full-stack web project:

### `.claude/skills/security-review.md`

```markdown
---
effort: high
disable-model-invocation: true
---

# Security Review Expert

Perform a thorough security audit of the code or feature described.

Check for:
- SQL injection and NoSQL injection
- Cross-site scripting (XSS)
- Cross-site request forgery (CSRF)
- Authentication and authorization flaws
- Sensitive data exposure
- Insecure direct object references
- Missing rate limiting

Output a risk matrix table with severity, likelihood, and remediation steps.
```

### `.claude/skills/performance-audit.md`

```markdown
---
effort: high
---

# Performance Audit Expert

Analyze the specified code or feature for performance issues.

Check for:
- N+1 database queries
- Missing indexes
- Unnecessary re-renders (React)
- Large bundle imports
- Unoptimized images and assets
- Missing caching opportunities
- Memory leaks

Provide benchmarks where possible and concrete optimization code.
```

### `.claude/skills/quick-explain.md`

```markdown
---
effort: low
---

# Quick Explainer

Give a brief, clear explanation of the code or concept described.
Keep it under 200 words. Use one code example if helpful.
Skip background context --- assume the reader is an experienced developer.
```

---

## Best Practices

1. **Keep skills focused** --- one skill per domain of expertise. Do not combine security review and performance audit into a single skill.
2. **Use `disable-model-invocation: true`** for high-cost or sensitive skills so they only run when you explicitly request them.
3. **Set appropriate effort levels** --- use `low` for quick lookups, `high` for thorough analysis.
4. **Document what triggers the skill** --- add a comment at the top explaining when to use it.
5. **Version skills in git** --- like custom commands, project skills should be committed and reviewed.
6. **Prefer skills over bloated CLAUDE.md** --- if your CLAUDE.md is growing past 100 lines, move specialized sections into skills.

---

## Navigation

| Direction | Link |
|-----------|------|
| Previous | [Custom Commands](custom-commands.md) |
| Next | [Module 07: Advanced Features](../07-advanced-features/) |
| Module Home | [Module 06 Overview](README.md) |
