# Subagents & Parallel Work

**Module 07, Lesson 4 — Claude Code Mastery**

**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Overview

Subagents are isolated Claude instances that your main session can spawn to handle tasks in parallel. Each subagent gets its own context window, runs independently, and reports results back to the parent session. This lesson covers the different subagent types, when to use them, how worktree isolation works, and the cost implications of parallel work.

---

## What Are Subagents?

A subagent is a separate Claude session launched by the main agent to perform a specific task. Think of it like delegating work to a colleague — you describe what you need, they go off and do it, and they report back when finished.

Key characteristics:

- **Isolated context** — Each subagent has its own context window, separate from the parent
- **Parallel execution** — Multiple subagents can run simultaneously
- **Scoped permissions** — Subagents inherit the parent's tool permissions
- **Result reporting** — Output is summarized and returned to the parent session

---

## The Agent Tool

Claude Code uses the **Agent tool** internally to dispatch subagents. When Claude determines that a task benefits from isolation or parallelism, it launches one or more subagents automatically.

You can also prompt this behavior explicitly:

```bash
> Research the authentication patterns in src/auth/ and the database
> schema in src/models/ in parallel, then recommend an approach.
```

Claude may spawn two subagents — one to explore auth patterns and one to analyze the database schema — then synthesize their findings.

---

## Subagent Types

| Type | Purpose | When Used |
|------|---------|-----------|
| **General-purpose** | Perform any coding task | Multi-file edits, complex research, broad investigations |
| **Explore** | Read-only investigation | Codebase exploration, finding patterns, answering questions about code |
| **Plan** | Create a structured plan | Breaking down complex tasks, generating step-by-step approaches |
| **claude-code-guide** | Answer questions about Claude Code itself | Help with configuration, commands, and features |

### General-Purpose Subagents

These are full-capability agents that can read files, write code, run commands, and use all available tools. They are dispatched for tasks that require making changes or performing substantial work.

### Explore Subagents

Explore subagents are read-only — they can search and read files but cannot make modifications. This makes them safe for research tasks where you want information without risk of unintended changes.

### Plan Subagents

Plan subagents analyze a problem and produce a structured plan without executing it. Use these when you want to review an approach before committing to implementation.

### claude-code-guide Subagents

These specialized subagents have knowledge about Claude Code itself and can answer questions about features, configuration, and best practices.

---

## Separate Context Windows

Each subagent operates in its own context window. This is significant because:

- The parent session does not lose context when subagents read large files
- Subagents can explore deeply without polluting the main conversation
- Multiple subagents can each work with a full context window simultaneously

```
Parent Session (200K context)
├── Subagent A (200K context) — exploring auth code
├── Subagent B (200K context) — analyzing database schema
└── Subagent C (200K context) — reviewing test coverage
```

The parent receives a summarized result from each subagent, not the full conversation. This keeps the parent's context lean.

---

## Worktree Isolation

For subagents that modify files, Claude Code uses **git worktrees** to provide filesystem isolation:

```bash
# Claude Code creates a temporary worktree for each writing subagent
git worktree add /tmp/claude-worktree-abc123 HEAD
```

**How worktree isolation works:**

1. Claude Code creates a new git worktree from the current branch
2. The subagent makes all changes in the worktree, not the main working directory
3. When the subagent completes, changes are merged back or presented for review
4. The temporary worktree is cleaned up

**Benefits:**

- Multiple subagents can edit the same files without conflicts
- Failed subagent work does not affect the main working directory
- Changes can be reviewed before being applied

---

## When to Use Subagents vs Direct Tools

| Scenario | Approach | Reason |
|----------|----------|--------|
| Edit a single file | Direct tools | No need for isolation overhead |
| Read a specific function | Direct tools | Simple, fast |
| Explore an unfamiliar codebase | Explore subagent | Keeps parent context clean |
| Make changes across 10+ files | General subagent | Benefits from isolation and parallel work |
| Plan a large refactor | Plan subagent | Get a reviewable plan before executing |
| Research two independent areas | Two Explore subagents | Parallel investigation saves time |
| Quick question about Claude Code | claude-code-guide | Specialized knowledge |

**Rule of thumb:** If a task is simple and affects few files, use direct tools. If a task is complex, touches many files, or can be parallelized, use subagents.

---

## Cost Implications

Subagents consume tokens independently. Each subagent incurs:

- **Input tokens** for its system prompt and the task description
- **Output tokens** for its reasoning and responses
- **Tool-use tokens** for file reads, searches, and commands

| Pattern | Approximate Cost |
|---------|-----------------|
| Single direct tool call | 1x |
| One subagent for research | 3–5x a direct call |
| Three parallel subagents | 10–15x a direct call |
| Complex multi-subagent orchestration | 20–30x a direct call |

**Cost management tips:**

- Use Explore subagents (read-only) when you do not need write capability
- Prefer Plan subagents to scope work before launching expensive general subagents
- Avoid spawning subagents for tasks that a single tool call can handle
- Monitor session costs with `/cost` to track subagent spending
- Use lower effort levels for subagent tasks when deep reasoning is unnecessary

---

## Practical Example

A typical multi-subagent workflow:

```bash
> I need to add rate limiting to our API. Research the current
> middleware stack, check how other services handle rate limiting,
> and propose an implementation plan.

# Claude might:
# 1. Launch Explore subagent → analyze src/middleware/
# 2. Launch Explore subagent → search for existing rate limiting code
# 3. Launch Plan subagent → create implementation plan from findings
# 4. Present the consolidated plan to you for review
```

This approach keeps the parent session's context focused on the high-level conversation while subagents handle the deep research.

---

## Summary

Subagents extend Claude Code's capabilities by providing isolated, parallel workers with their own context windows. Use Explore subagents for safe research, Plan subagents for structured planning, and general subagents for complex multi-file work. Worktree isolation protects your working directory from subagent modifications. Be mindful of cost — each subagent is a separate Claude session — and use them strategically for tasks that genuinely benefit from isolation or parallelism.

---

[← Back to Module Overview](README.md)

[← Previous Module](../06-hooks-mcp-commands/) | [Course Home](../../README.md) | [Next Module →](../08-multi-platform/)
