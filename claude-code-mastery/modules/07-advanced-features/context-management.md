# Context Window Management

**Module 07, Lesson 3 — Claude Code Mastery**

**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Overview

Every Claude Code session operates within a finite context window. Everything you say, every file Claude reads, every tool output, and every CLAUDE.md file consumes tokens from that window. When context fills up, quality degrades and eventually the session cannot continue. This lesson teaches you how to monitor, manage, and optimize context usage so your sessions remain productive from start to finish.

---

## What Uses Context

| Source | Token Impact | Notes |
|--------|-------------|-------|
| Conversation messages | Medium | Your prompts and Claude's responses accumulate |
| File reads | High | Large files consume significant context |
| Tool outputs | Medium–High | Command output, search results, diffs |
| CLAUDE.md files | Low–Medium | Loaded at session start and after compaction |
| MCP tool definitions | Low–Medium | Each registered tool adds schema tokens |
| System prompts | Low | Fixed overhead per session |

A single large file read (5,000+ lines) can consume 10–20% of a standard 200K context window. Be selective about what you ask Claude to read.

---

## The /compact Command

The `/compact` command summarizes the current conversation and replaces it with a compressed version, freeing context for new work.

```bash
> /compact
# Summarizes the entire conversation

> /compact focus on the database migration work
# Summarizes with emphasis on a specific topic
```

The optional focus argument tells Claude what to prioritize when compressing. Use it when your session covered multiple topics but you only need to continue one thread.

**What /compact preserves:**

- Key decisions and conclusions
- File paths that were modified
- Outstanding tasks and next steps
- Context specified in the focus argument

**What /compact discards:**

- Intermediate reasoning and exploration
- Raw file contents that were read
- Verbose tool outputs
- Abandoned approaches

---

## Auto-Compaction

Claude Code automatically compacts the conversation when the context window reaches approximately 95% capacity. This prevents session failure but may discard context you still need.

To stay ahead of auto-compaction:

- Run `/compact` manually before hitting the limit
- Use a focus argument to control what gets preserved
- Switch to a 1M context model for large tasks (`/model opus[1m]`)

---

## The /context Command

The `/context` command shows your current context window usage:

```bash
> /context
# Displays: tokens used, tokens remaining, percentage filled
```

Check this periodically during long sessions, especially before starting a large file read or multi-step operation.

---

## The /clear Command

The `/clear` command resets the session entirely, starting fresh with an empty conversation:

```bash
> /clear
# Wipes all conversation history — starts clean
```

Use `/clear` when switching to an unrelated task within the same terminal. It is more aggressive than `/compact` — nothing from the previous conversation is preserved.

---

## Session Management

### Naming Sessions

```bash
> /rename database-migration
# Names the current session for easy identification
```

### Resuming Sessions

```bash
claude --resume database-migration
# Resumes a previously named session

claude --continue
# Continues the most recent session
```

Named sessions persist across terminal restarts. Use them for multi-day tasks where you need to pick up exactly where you left off.

---

## MCP Overhead and How to Reduce It

Each MCP server registers tool definitions that consume context tokens. A server with 30 tools can add several thousand tokens of overhead to every session.

**Strategies to reduce MCP overhead:**

| Strategy | How |
|----------|-----|
| Limit active servers | Only enable servers you need for the current task |
| Use project-level config | Configure MCP servers per-project, not globally |
| Prefer fewer, focused servers | One server with 5 tools beats five servers with 1 tool each |
| Disable unused servers | Remove servers from settings when not actively using them |

---

## Tool Search for Large Tool Sets

When many MCP servers are active, Claude Code uses **tool search** instead of loading all tool schemas into context. Tool search indexes available tools and retrieves only the relevant schemas when needed.

This is automatic when the total number of registered tools exceeds a threshold. You do not need to configure it, but you should be aware that:

- Tool search adds a small latency to the first use of a tool
- Rarely-used tools may not be found if their descriptions are unclear
- Well-named, well-described tools are discovered more reliably

---

## Code Intelligence Plugins

Claude Code can use language-aware code intelligence plugins to navigate codebases more efficiently, reducing the number of raw file reads needed:

- **Go to definition** — Jump to where a symbol is defined
- **Find references** — Locate all usages of a symbol
- **Symbol search** — Find symbols by name across the project

These features reduce context usage by letting Claude target specific code locations instead of reading entire files.

---

## Proactive Context Management Tips

1. **Start with a plan** — Outline your task before diving in, so Claude does not explore unnecessary files
2. **Read selectively** — Ask Claude to read specific functions or line ranges, not entire files
3. **Compact early** — Run `/compact` after completing a subtask, before starting the next
4. **Use subagents** — Delegate research tasks to subagents, which have their own context windows
5. **Check /context regularly** — Monitor usage every 15–20 minutes during intensive sessions
6. **Split large tasks** — Break multi-step work into separate sessions with `--resume`
7. **Minimize CLAUDE.md size** — Keep project instructions concise; verbose CLAUDE.md files waste tokens every session
8. **Choose the right model** — Use 1M context models for tasks that genuinely require broad awareness

---

## Summary

Context is your most constrained resource in Claude Code. Every file read, tool call, and message consumes tokens that cannot be recovered without compaction. Use `/context` to monitor, `/compact` to reclaim, and `/clear` to reset. Keep MCP overhead lean, leverage code intelligence to avoid unnecessary reads, and split large tasks across sessions. Proactive context management is what separates a smooth, productive session from one that degrades halfway through.

---

[← Back to Module Overview](README.md)

[← Previous Module](../06-hooks-mcp-commands/) | [Course Home](../../README.md) | [Next Module →](../08-multi-platform/)
