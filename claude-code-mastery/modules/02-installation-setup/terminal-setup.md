# Terminal Setup & Configuration

**Module 02, Lesson 4 — Claude Code Mastery**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Claude Code works in any terminal, but some terminals need configuration for the best experience. This lesson covers terminal setup, status line, and shell integration.

---

## Supported Terminals

### Full Support (No Setup Needed)

These terminals support `Shift+Enter` for multiline input out of the box:

| Terminal | Platform | Notes |
|----------|----------|-------|
| **iTerm2** | macOS | Recommended for macOS |
| **WezTerm** | Cross-platform | Excellent performance |
| **Ghostty** | macOS/Linux | Modern, fast |
| **Kitty** | macOS/Linux | GPU-accelerated |

### Requires Setup

These terminals need `/terminal-setup` for multiline input:

| Terminal | Platform | Setup Required |
|----------|----------|---------------|
| **VS Code Terminal** | Cross-platform | Run `/terminal-setup` |
| **Alacritty** | Cross-platform | Run `/terminal-setup` |
| **Zed** | macOS | Run `/terminal-setup` |
| **Warp** | macOS | Run `/terminal-setup` |

### Running Terminal Setup

Inside Claude Code:

```
/terminal-setup
```

This configures `Shift+Enter` keybinding for your terminal. Follow the on-screen instructions.

---

## Status Line

The status line shows useful information at the bottom of your terminal.

### Enable Status Line

```
/statusline
```

Or configure manually in `~/.claude.json`:

```json
{
  "statusLine": "{{model}} | {{gitBranch}} | Context: {{contextUsagePercent}}% | ${{costUSD}}"
}
```

### Available Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `{{model}}` | Current model | `sonnet` |
| `{{gitBranch}}` | Git branch | `main` |
| `{{contextUsagePercent}}` | Context window usage | `42` |
| `{{tokenUsage}}` | Total tokens used | `15234` |
| `{{costUSD}}` | Session cost (API users) | `0.45` |
| `{{sessionDuration}}` | Time elapsed | `12m` |
| `{{effortLevel}}` | Thinking effort | `medium` |

### Example Status Lines

**Minimal:**
```json
{"statusLine": "{{model}} {{gitBranch}}"}
```

**Developer:**
```json
{"statusLine": "{{model}} ({{effortLevel}}) | {{gitBranch}} | {{contextUsagePercent}}% context"}
```

**Cost-conscious:**
```json
{"statusLine": "{{model}} | ${{costUSD}} | {{contextUsagePercent}}% | {{sessionDuration}}"}
```

---

## Shell Configuration

### Recommended Shell Settings

Add to your `~/.bashrc` or `~/.zshrc`:

```bash
# Claude Code alias
alias cc="claude"

# Start Claude Code in a specific directory
alias ccw="cd ~/workspace && claude"

# Resume last session
alias ccr="claude --resume"

# Continue last session
alias ccc="claude --continue"
```

### Environment Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `ANTHROPIC_API_KEY` | API key for authentication | `sk-ant-api03-xxx` |
| `ANTHROPIC_MODEL` | Default model | `sonnet` |
| `CLAUDE_CODE_EFFORT_LEVEL` | Default thinking effort | `medium` |
| `CLAUDE_CONFIG_DIR` | Custom config directory | `/custom/path` |
| `CLAUDE_CODE_DISABLE_1M_CONTEXT` | Disable 1M context | `1` |
| `ENABLE_TOOL_SEARCH` | Tool search threshold | `auto:5` |

---

## Vim Mode

Enable vim-style keybindings for the input prompt:

```
/vim
```

Or set in config:

```
/config
# Set editorMode to "vim"
```

Vim mode gives you normal/insert mode switching, motions (`w`, `b`, `e`, `0`, `$`), text objects (`iw`, `i"`, `i(`), and editing commands (`dd`, `cc`, `yy`, `p`). Full details in Module 03.

---

## Notifications

Configure desktop notifications for when Claude needs your attention:

### macOS

Add to your settings:

```json
{
  "hooks": {
    "Notification": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "osascript -e 'display notification \"Claude Code needs your attention\" with title \"Claude Code\"'"
          }
        ]
      }
    ]
  }
}
```

### Linux

```json
{
  "hooks": {
    "Notification": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "notify-send 'Claude Code' 'Needs your attention'"
          }
        ]
      }
    ]
  }
}
```

---

**Next:** [Your First Claude Code Session](first-session.md)

[← Back to Module Overview](README.md)

---

*Module 02, Lesson 4 — Claude Code Mastery — March 2026*
