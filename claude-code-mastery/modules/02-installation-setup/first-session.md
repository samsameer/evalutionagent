# Your First Claude Code Session

**Module 02, Lesson 5 — Claude Code Mastery**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Let's walk through your first real Claude Code session step by step. You'll learn how to navigate the interface, give instructions, approve actions, and get productive work done.

---

## Step 1: Navigate to Your Project

```bash
cd ~/your-project
claude
```

> **Important:** Always run `claude` from your project's root directory. Claude Code uses the current directory as its working context.

---

## Step 2: The Interface

When Claude Code starts, you'll see:

```
╭──────────────────────────────────────────────╮
│  Claude Code v2.8.x                          │
│  Model: sonnet                               │
│  Working directory: ~/your-project           │
│                                              │
│  Type your message and press Enter to send.  │
│  Press Shift+Enter for multiline input.      │
│  Type /help for available commands.           │
╰──────────────────────────────────────────────╯

>
```

### Interface Elements

- **Input area** — Where you type your messages (bottom)
- **Response area** — Where Claude's responses appear (above)
- **Tool calls** — Shown as collapsible blocks
- **Permission prompts** — Appear when Claude needs approval
- **Status bar** — Shows model, mode, context usage (if enabled)

---

## Step 3: Your First Prompt

Try something simple:

```
> Explain the structure of this project
```

Claude will:
1. Read key files (README, package.json, etc.)
2. Scan the directory structure
3. Provide a summary of your project

---

## Step 4: Understanding Permission Prompts

When Claude wants to take an action, you'll see a prompt:

```
Claude wants to run: cat package.json

  [y] Allow  [n] Deny  [a] Always allow  [Esc] Cancel
```

Your options:

| Key | Action | Effect |
|-----|--------|--------|
| `y` | Allow once | Approves this single action |
| `n` | Deny | Blocks this action |
| `a` | Always allow | Adds to your allowed tools for this session |
| `Esc` | Cancel | Cancels the current task |

---

## Step 5: Try a Real Task

Here are some great first tasks to try:

### Read and Understand

```
> What does the main function do in this project?
```

### Find a Bug

```
> Are there any potential bugs in the error handling?
```

### Make a Change

```
> Add a .gitignore file with common Node.js entries
```

### Run a Command

```
> Run the tests and tell me if anything fails
```

---

## Step 6: Multiline Input

For complex prompts, use `Shift+Enter` to add new lines:

```
> I need you to do three things:
  1. Add input validation to the /api/users endpoint
  2. Write tests for the validation
  3. Update the API documentation
```

---

## Step 7: Essential Commands to Know

| Command | What It Does |
|---------|-------------|
| `/help` | Show all available commands |
| `/clear` | Clear conversation, start fresh |
| `/compact` | Compress context to free space |
| `/cost` | Show token usage and cost |
| `/model` | Switch AI model |
| `/memory` | View loaded memory files |
| `Ctrl+C` | Cancel current operation |
| `Ctrl+C × 2` | Exit Claude Code |

---

## Step 8: Initialize Project Memory

For best results, let Claude Code learn about your project:

```
> /init
```

This creates a `CLAUDE.md` file in your project root with:
- Build and test commands
- Project conventions
- Architecture overview
- Coding standards

---

## Common First-Session Tips

### Be Specific
- Instead of: "Fix the code"
- Try: "Fix the null pointer error in src/auth/login.ts on line 45"

### Provide Context
- Instead of: "Add a feature"
- Try: "Add a dark mode toggle to the settings page, using the existing ThemeContext"

### Let Claude Explore First
- "Read through the codebase and tell me about the architecture before making any changes"

### Use Plan Mode for Complex Tasks
- Press `Shift+Tab` to switch to plan mode
- Ask Claude to plan before executing

---

## What's Next?

You're now ready to use Claude Code productively. In the next module, we'll master every command, shortcut, and flag available.

---

**Next Module:** [Core Commands & Slash Commands →](../03-core-commands/)

[← Back to Module Overview](README.md) | [Course Home](../../README.md)

---

*Module 02, Lesson 5 — Claude Code Mastery — March 2026*
