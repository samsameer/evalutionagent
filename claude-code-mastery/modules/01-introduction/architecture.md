# Architecture — How Claude Code Works

**Module 01, Lesson 3 — Claude Code Mastery**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Understanding how Claude Code works under the hood will help you use it more effectively. This lesson explains the agentic loop, tool system, context window, and how Claude Code interacts with your environment.

---

## The Agentic Loop

Claude Code operates in a continuous **plan → act → observe → iterate** cycle:

```
┌──────────────────────────────────────────┐
│           YOUR PROMPT                     │
│   "Add input validation to the API"       │
└──────────────┬───────────────────────────┘
               │
               ▼
┌──────────────────────────────────────────┐
│         CLAUDE PLANS                      │
│   Reads codebase, identifies files,       │
│   determines approach                     │
└──────────────┬───────────────────────────┘
               │
               ▼
┌──────────────────────────────────────────┐
│         CLAUDE ACTS (Tool Use)            │
│   Read files → Edit code → Run tests      │
│   → Search for patterns → Write files     │
└──────────────┬───────────────────────────┘
               │
               ▼
┌──────────────────────────────────────────┐
│         CLAUDE OBSERVES                   │
│   Reviews tool output, checks for errors, │
│   verifies changes work correctly         │
└──────────────┬───────────────────────────┘
               │
               ▼
┌──────────────────────────────────────────┐
│         ITERATE OR COMPLETE               │
│   If issues found → back to PLAN          │
│   If done → present results to user       │
└──────────────────────────────────────────┘
```

Each step in this loop is a **turn**. Complex tasks may take 10-50+ turns to complete.

---

## The Context Window

The context window is the "working memory" that holds everything Claude can see at once.

### What Lives in the Context Window

| Component | Persistence | Size Impact |
|-----------|------------|-------------|
| System instructions | Always present | ~2-5K tokens |
| CLAUDE.md files | Always present | Varies (target <500 lines) |
| Auto-memory (first 200 lines) | Always present | ~1-2K tokens |
| MCP tool definitions | Always present | ~500-2K per server |
| Conversation history | Grows over time | Main cost driver |
| File contents (from Read) | Until compacted | Can be large |
| Command outputs (from Bash) | Until compacted | Can be large |
| Thinking tokens | Per-turn only | Not persisted |

### Context Window Sizes

| Model | Standard | Extended |
|-------|----------|----------|
| Opus 4.6 | 200K tokens | 1M tokens |
| Sonnet 4.6 | 200K tokens | 1M tokens |
| Haiku 4.5 | 200K tokens | N/A |

### How Context is Managed

1. **Auto-compaction** — When context fills up, Claude automatically summarizes older conversation
2. **Manual compaction** — Use `/compact` to free space
3. **Tool output clearing** — Older tool outputs are removed first
4. **CLAUDE.md preservation** — Memory files survive compaction (re-read from disk)

---

## The Tool System

Claude Code has access to a set of **built-in tools** that let it interact with your environment:

### Core Tools

```
┌─────────────────────────────────────────────────┐
│                  CLAUDE CODE                      │
│                                                   │
│   ┌─────────┐  ┌─────────┐  ┌─────────┐         │
│   │  Read   │  │  Edit   │  │  Write  │         │
│   │ (files) │  │ (files) │  │ (files) │         │
│   └─────────┘  └─────────┘  └─────────┘         │
│                                                   │
│   ┌─────────┐  ┌─────────┐  ┌─────────┐         │
│   │  Bash   │  │  Glob   │  │  Grep   │         │
│   │(commands)│  │(find)   │  │(search) │         │
│   └─────────┘  └─────────┘  └─────────┘         │
│                                                   │
│   ┌──────────┐  ┌───────────┐  ┌─────────┐      │
│   │ WebFetch │  │ WebSearch │  │  Agent  │      │
│   │  (URLs)  │  │  (web)    │  │(subagent)│      │
│   └──────────┘  └───────────┘  └─────────┘      │
│                                                   │
│   ┌───────────┐  ┌─────────────┐                 │
│   │ TodoWrite │  │ MCP Tools   │                 │
│   │ (tracking)│  │ (external)  │                 │
│   └───────────┘  └─────────────┘                 │
└─────────────────────────────────────────────────┘
```

### How Tool Calls Work

1. Claude decides which tool to use based on the task
2. Claude formats the tool call with parameters
3. The permission system checks if the action is allowed
4. If allowed (or user approves), the tool executes
5. The result is returned to Claude's context
6. Claude processes the result and decides the next step

### The Permission Layer

```
Claude wants to run: npm test
    │
    ▼
Permission Check:
    ├── Is Bash(npm test) in allowedTools? → Auto-approve
    ├── Is Bash(npm*) in allowedTools? → Auto-approve
    ├── Is Bash in denyTools? → Auto-deny
    ├── Permission mode = acceptEdits? → Prompt user
    ├── Permission mode = bypassPermissions? → Auto-approve
    └── Default → Prompt user for approval
```

---

## Communication Architecture

```
┌──────────────┐         ┌──────────────┐
│  Your        │  HTTPS  │  Anthropic   │
│  Terminal    │◄───────►│  API         │
│  (Claude CLI)│         │  (Claude AI) │
└──────┬───────┘         └──────────────┘
       │
       │  Local access
       ▼
┌──────────────────────────────────────┐
│           YOUR MACHINE                │
│                                       │
│  ┌──────────┐  ┌──────────────────┐  │
│  │ Files    │  │ Terminal/Shell   │  │
│  │ (read/   │  │ (bash commands)  │  │
│  │  write)  │  │                  │  │
│  └──────────┘  └──────────────────┘  │
│                                       │
│  ┌──────────┐  ┌──────────────────┐  │
│  │ Git      │  │ MCP Servers      │  │
│  │ (version │  │ (external tools) │  │
│  │  control)│  │                  │  │
│  └──────────┘  └──────────────────┘  │
└──────────────────────────────────────┘
```

### Key Points

- **Claude Code runs locally** — The CLI runs on your machine
- **Code stays local** — Your files are never uploaded to Anthropic's servers
- **API calls send context** — Only the conversation and tool results are sent
- **Responses stream back** — Claude's responses stream in real-time
- **MCP servers are local** — MCP processes run on your machine

---

## Session Management

### Session Lifecycle

```
claude                    # Start new session
  │
  ├── Work on tasks...
  │
  ├── /compact            # Free context space
  │
  ├── /clear              # End session, start fresh
  │
  └── Exit (Ctrl+C × 2)  # Exit CLI
```

### Session Persistence

- **Sessions are saved** — Every conversation is stored locally
- **Resume sessions** — `claude --resume` or `claude --continue`
- **Named sessions** — Use `/rename` to give sessions descriptive names
- **Session history** — Browse with `claude --resume` (interactive picker)

### Storage Locations

| Data | Location |
|------|----------|
| Sessions | `~/.claude/projects/<project>/sessions/` |
| Auto-memory | `~/.claude/projects/<project>/memory/` |
| Credentials | `~/.claude/.credentials.json` (Linux) or Keychain (macOS) |
| Settings | `~/.claude/settings.json` |
| Config | `~/.claude.json` |

---

## Summary

Claude Code is not just a chatbot — it's an **autonomous agent** that:

1. **Plans** — Analyzes your request and codebase
2. **Acts** — Uses tools to read, write, search, and execute
3. **Observes** — Reviews results and checks for errors
4. **Iterates** — Fixes issues and continues until done

Understanding this loop helps you write better prompts, manage context efficiently, and get the most out of Claude Code.

---

**Next Module:** [Installation & Setup →](../02-installation-setup/)

[← Back to Module Overview](README.md) | [Course Home](../../README.md)

---

*Module 01, Lesson 3 — Claude Code Mastery — March 2026*
