# Module 01: Introduction to Claude Code

**Claude Code Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Module Overview

Claude Code is Anthropic's **agentic coding tool** — a terminal-native AI assistant that doesn't just answer questions, it **writes code, edits files, runs commands, searches the web, and manages your entire development workflow** directly from your CLI.

Unlike traditional AI chatbots or code completion tools, Claude Code operates as an autonomous agent. Give it a task, and it will plan, execute, debug, and iterate until the job is done. It reads your codebase, understands your project structure, and makes changes with full context awareness.

In this module, you'll learn what Claude Code is, how it compares to other tools, what powers it under the hood, and which plan is right for you.

---

## Learning Objectives

- Understand what Claude Code is and why it's different from chatbots and code completions
- Learn the difference between Claude Code, Claude.ai, and Claude Desktop
- Compare subscription plans and choose the right one
- Understand the AI models (Opus 4.6, Sonnet 4.6, Haiku 4.5) powering Claude Code

---

## Lessons

| Lesson | Topic | Description |
|--------|-------|-------------|
| 1 | [What is Claude Code?](README.md) | This page — overview, history, and comparison |
| 2 | [Plans, Pricing & Model Comparison](plans-and-pricing.md) | Pro, Max, Team, Enterprise, API breakdown |
| 3 | [Architecture — How Claude Code Works](architecture.md) | Under the hood: tools, context, and agentic loop |

---

## What is Claude Code?

Claude Code is a **command-line interface (CLI) tool** developed by Anthropic that brings Claude's intelligence directly into your terminal. It is:

- **Terminal-native** — Lives in your CLI, not a browser
- **Agentic** — Plans and executes multi-step tasks autonomously
- **Context-aware** — Reads your entire codebase, understands project structure
- **Tool-using** — Can edit files, run commands, search code, browse the web
- **Git-integrated** — Creates commits, branches, and pull requests
- **Multi-platform** — Available as CLI, VS Code extension, JetBrains plugin, web app, and desktop app

### What Makes Claude Code Different?

| Feature | Traditional Chatbot | Code Completion | Claude Code |
|---------|-------------------|-----------------|-------------|
| Understands full codebase | No | Partial | Yes |
| Edits multiple files | No | No | Yes |
| Runs terminal commands | No | No | Yes |
| Creates git commits/PRs | No | No | Yes |
| Browses the web | No | No | Yes |
| Autonomous multi-step tasks | No | No | Yes |
| Works in your terminal | No | Yes (editor) | Yes |
| Remembers project context | No | Limited | Yes (CLAUDE.md) |

### Claude Code vs. Other Anthropic Products

| Product | What It Is | Best For |
|---------|-----------|----------|
| **Claude.ai** | Web-based chat interface | General conversations, writing, analysis |
| **Claude Desktop** | Desktop app with computer use | Business automation, file management |
| **Claude Cowork** | Agent in Claude Desktop | Non-technical business workflows |
| **Claude Code** | CLI coding tool | Software development, DevOps, engineering |
| **Claude API** | Programmatic access | Building AI-powered applications |
| **Claude Agent SDK** | SDK for custom agents | Building custom coding agents |

### A Brief History of Claude Code

| Date | Milestone |
|------|-----------|
| February 2025 | Claude Code launched as research preview |
| March 2025 | General availability — production-ready release |
| April 2025 | VS Code and JetBrains extensions launched |
| May 2025 | Hooks system and custom slash commands added |
| June 2025 | MCP server integration |
| August 2025 | Claude Code on the web (claude.ai/code) launched |
| October 2025 | Agent SDK released |
| November 2025 | Auto mode (background safety classifier) |
| January 2026 | Desktop app for Mac and Windows |
| March 2026 | Adaptive reasoning, 1M context, enhanced subagents (v2.8+) |

### What Can Claude Code Do?

Here are real examples of what you can accomplish:

> **"Add authentication to my Express app using JWT tokens"**

Claude Code will:
1. Read your existing codebase
2. Install required packages (`jsonwebtoken`, `bcrypt`)
3. Create auth middleware, login/register routes
4. Update your existing routes to use the middleware
5. Add tests
6. Create a git commit with a descriptive message

> **"Find and fix the bug causing the 500 error on /api/users"**

Claude Code will:
1. Search your codebase for the relevant route
2. Read the handler code and related files
3. Identify the root cause
4. Fix the code
5. Run your tests to verify the fix

> **"Refactor the database layer to use connection pooling"**

Claude Code will:
1. Analyze your current database code across all files
2. Plan the refactoring approach
3. Make changes across multiple files
4. Update configuration
5. Run tests and fix any issues

---

## Key Concepts

### The Agentic Loop

Claude Code operates in an **agentic loop**:

```
You give a task
    → Claude plans the approach
        → Claude uses tools (read, edit, bash, search)
            → Claude reviews results
                → Claude iterates if needed
                    → Claude presents the result
```

### Tools Available to Claude Code

| Tool | What It Does |
|------|-------------|
| **Read** | Read any file in your project |
| **Edit** | Make precise edits to existing files |
| **Write** | Create new files |
| **Bash** | Execute shell commands |
| **Glob** | Find files by pattern |
| **Grep** | Search file contents |
| **WebFetch** | Fetch content from URLs |
| **WebSearch** | Search the web |
| **Agent** | Spawn sub-agents for parallel work |
| **TodoWrite** | Track multi-step task progress |

### The Permission System

Claude Code asks for permission before taking potentially dangerous actions:

- **File edits** — Claude asks before modifying your code (configurable)
- **Shell commands** — Claude asks before running terminal commands (configurable)
- **Web requests** — Claude asks before fetching external URLs
- **MCP tools** — Claude asks before using external tool integrations

You control the level of autonomy through **permission modes** (covered in Module 03).

---

## Next Steps

Continue to the next lesson to understand pricing and choose the right plan:

**Next:** [Plans, Pricing & Model Comparison](plans-and-pricing.md)

---

[Back to Course Home](../../README.md) | [Next Module: Installation & Setup →](../02-installation-setup/)

---

*Module 01 — Claude Code Mastery — March 2026*
