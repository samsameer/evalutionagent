# All Slash Commands Reference

**Module 03, Lesson 2 — Claude Code Mastery**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Slash commands are typed directly in the Claude Code input prompt. They start with `/` and trigger specific actions. Here is every slash command available.

---

## Complete Slash Commands Table

| Command | Description | Category |
|---------|-------------|----------|
| `/bug` | Report a bug to Anthropic | Support |
| `/clear` | Clear conversation and start fresh | Session |
| `/compact` | Compress conversation to free context | Context |
| `/compact [focus]` | Compress with specific focus area | Context |
| `/config` | Open configuration settings | Settings |
| `/context` | Show context window usage details | Context |
| `/cost` | Show token usage and cost for current session | Monitoring |
| `/doctor` | Run diagnostics on installation and config | Troubleshooting |
| `/effort` | Set thinking effort level (low/medium/high/max/auto) | Thinking |
| `/fast` | Toggle fast mode (same model, faster output) | Performance |
| `/help` | Show available commands and usage help | Help |
| `/init` | Initialize CLAUDE.md for your project | Memory |
| `/listen` | Enter listen mode for external triggers | Integration |
| `/login` | Authenticate with Anthropic | Auth |
| `/logout` | Sign out of current account | Auth |
| `/mcp` | Manage MCP servers (view, enable, disable) | MCP |
| `/memory` | Browse and manage loaded memory files | Memory |
| `/model` | Switch AI model (interactive picker) | Model |
| `/model [name]` | Switch to specific model directly | Model |
| `/permissions` | View and manage tool permissions | Permissions |
| `/rename [name]` | Rename current session | Session |
| `/review` | Get a code review of current changes | Code Review |
| `/statusline` | Configure terminal status line | Terminal |
| `/terminal-setup` | Configure terminal for Shift+Enter | Terminal |
| `/vim` | Toggle vim mode for input editing | Editor |

---

## Detailed Command Guide

### `/clear` — Clear Conversation

Starts a fresh conversation while keeping the session saved.

```
/clear
```

> **Tip:** Use `/clear` when switching between unrelated tasks. Your previous session is still accessible via `claude --resume`.

### `/compact` — Compress Context

Frees up context window space by summarizing older conversation.

```
/compact                              # Auto-summarize
/compact focus on the API changes     # Guided summary
/compact keep the test results        # Preserve specific info
```

**When to use:**
- Context window is filling up (check with `/context`)
- Moving from research to implementation
- Long debugging sessions with lots of output

**What survives compaction:**
- CLAUDE.md files (re-read from disk)
- Key decisions and outcomes
- Recent conversation

**What may be lost:**
- Detailed tool outputs from early conversation
- Verbose command results
- Specific instructions only mentioned in conversation (put these in CLAUDE.md!)

### `/config` — Settings

Opens interactive settings menu:

```
/config
```

Available settings include:
- Theme (light/dark)
- Editor mode (normal/vim)
- Extended thinking toggle
- Auto-memory toggle
- Notification preferences

### `/cost` — Usage Statistics

Shows current session costs (for API users):

```
/cost
```

Output:
```
Total cost:     $2.45
API duration:   4m 32s
Wall duration:  12m 15s
Code changes:   +145 / -23 lines
```

> **Note:** Subscription users (Pro/Max/Team) see usage in `/stats` instead.

### `/doctor` — Diagnostics

Runs comprehensive health checks:

```
/doctor
```

Checks:
- Installation integrity
- Authentication status
- Permission configuration
- Hook configuration
- MCP server connectivity
- Git setup
- Keybinding warnings
- Network connectivity

### `/effort` — Thinking Depth

Control how deeply Claude thinks before responding:

```
/effort low       # Fast, minimal thinking
/effort medium    # Balanced (default)
/effort high      # Deep analysis
/effort max       # Maximum reasoning (Opus only, slowest)
/effort auto      # Reset to model default
```

### `/init` — Initialize Project Memory

Analyzes your codebase and creates a CLAUDE.md file:

```
/init
```

Claude will:
1. Scan your project structure
2. Identify build/test commands
3. Discover coding conventions
4. Create a CLAUDE.md with project-specific instructions

If CLAUDE.md already exists, `/init` suggests improvements.

### `/memory` — Memory Browser

Interactive viewer for all loaded memory files:

```
/memory
```

Shows:
- All loaded CLAUDE.md files and locations
- Rules from `.claude/rules/`
- Auto-memory status (toggle on/off)
- Open any file in your editor

### `/model` — Model Switcher

Interactive model picker:

```
/model            # Opens interactive picker with effort slider
/model opus       # Switch directly to Opus
/model sonnet     # Switch directly to Sonnet
/model haiku      # Switch directly to Haiku
/model opus[1m]   # Opus with 1M context
/model sonnet[1m] # Sonnet with 1M context
```

In the interactive picker, use left/right arrows to adjust the effort level.

### `/review` — Code Review

Get an AI code review of your current changes:

```
/review
```

Claude analyzes your uncommitted changes and provides:
- Potential bugs
- Security issues
- Performance concerns
- Code quality suggestions

### `/vim` — Vim Mode

Toggle vim-style keybindings:

```
/vim
```

When enabled, the input area supports:
- Normal/Insert mode switching (`Esc` / `i`)
- Motions (`w`, `b`, `e`, `0`, `$`, `gg`, `G`)
- Editing (`dd`, `cc`, `yy`, `p`, `x`)
- Text objects (`iw`, `i"`, `i(`, `i{`)
- Repeat (`.`)

---

## Custom Slash Commands

You can create your own slash commands. See [Module 06: Custom Commands](../06-hooks-mcp-commands/custom-commands.md) for details.

---

**Next:** [Keyboard Shortcuts](keyboard-shortcuts.md)

[← Back to Module Overview](README.md)

---

*Module 03, Lesson 2 — Claude Code Mastery — March 2026*
