# The Hooks System

**Module 06, Lesson 1 — Claude Code Mastery**

**Instructor: Jabbir Basha, Principal AI Engineer**

---

## What Are Hooks?

Hooks are user-defined shell commands that Claude Code executes at specific points during its lifecycle. They let you intercept, validate, log, and extend Claude's behavior — without modifying Claude itself. Hooks run **synchronously** and can block or modify tool execution.

Hooks are configured in your settings files (`~/.claude/settings.json` for global, `.claude/settings.json` for project-level).

---

## Hook Types Reference

| Hook Type | Trigger Point | Can Block? | Use Case |
|-----------|--------------|------------|----------|
| `PreToolUse` | Before a tool executes | Yes | Validate commands, block dangerous operations |
| `PostToolUse` | After a tool completes | No | Auto-format, lint, log results |
| `Notification` | Claude needs user attention | No | Desktop alerts, sound notifications |
| `Stop` | Claude finishes responding | No | Summary logging, cleanup tasks |
| `SubagentStop` | A subagent finishes | No | Aggregate subagent results |
| `SessionStart` | Session initialization (web) | No | Environment setup, greeting |
| `WorktreeCreate` | Git worktree is created | No | Initialize worktree environment |
| `WorktreeRemove` | Git worktree is removed | No | Cleanup worktree artifacts |
| `InstructionsLoaded` | CLAUDE.md files are loaded | No | Debug which instruction files are active |

---

## Hook Configuration Structure

Hooks are defined in `settings.json` under the `"hooks"` key. Each hook type contains an array of matchers:

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "echo 'About to run bash command'"
          }
        ]
      }
    ]
  }
}
```

### Configuration Fields

| Field | Type | Description |
|-------|------|-------------|
| `matcher` | `string` | Tool name to match (e.g., `"Bash"`, `"Write"`, `"Edit"`). Empty string matches all tools. |
| `hooks` | `array` | List of hook actions to execute |
| `hooks[].type` | `string` | Always `"command"` for shell hooks |
| `hooks[].command` | `string` | Shell command to run |
| `hooks[].timeout` | `number` | Timeout in milliseconds (default: 60000) |

---

## Matchers In Detail

The `matcher` field filters which tool invocations trigger the hook:

| Matcher Value | Matches |
|---------------|---------|
| `"Bash"` | All Bash tool calls |
| `"Write"` | File write operations |
| `"Edit"` | File edit operations |
| `"Read"` | File read operations |
| `""` (empty) | Every tool call |
| `"Glob"` | File glob/search operations |

---

## Environment Variables Available to Hooks

Claude Code injects context into hook processes via environment variables:

### All Hooks

| Variable | Description |
|----------|-------------|
| `CLAUDE_SESSION_ID` | Current session identifier |
| `CLAUDE_PROJECT_DIR` | Absolute path to the project root |

### PreToolUse / PostToolUse Hooks

| Variable | Description |
|----------|-------------|
| `CLAUDE_TOOL_NAME` | Name of the tool being called (e.g., `Bash`, `Write`) |
| `CLAUDE_TOOL_INPUT` | JSON string of the tool's input parameters |
| `CLAUDE_TOOL_OUTPUT` | JSON string of the tool's output (PostToolUse only) |

### Notification Hooks

| Variable | Description |
|----------|-------------|
| `CLAUDE_NOTIFICATION_TYPE` | One of: `permission_prompt`, `idle_prompt`, `auth_success`, `elicitation_dialog` |
| `CLAUDE_NOTIFICATION_MESSAGE` | The notification content |

---

## Blocking Behavior (PreToolUse)

A `PreToolUse` hook can **block** a tool call by exiting with a non-zero status code:

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "python3 /scripts/validate-bash-command.py"
          }
        ]
      }
    ]
  }
}
```

- **Exit code 0**: Tool execution proceeds normally.
- **Non-zero exit code**: Tool execution is blocked. Stderr output is shown to Claude as the reason.

---

## Common Hook Recipes

### Recipe 1: Auto-Format on File Write

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write",
        "hooks": [
          {
            "type": "command",
            "command": "FILE=$(echo $CLAUDE_TOOL_INPUT | jq -r '.file_path'); if [[ \"$FILE\" == *.py ]]; then black \"$FILE\" 2>/dev/null; elif [[ \"$FILE\" == *.js || \"$FILE\" == *.ts ]]; then npx prettier --write \"$FILE\" 2>/dev/null; fi"
          }
        ]
      }
    ]
  }
}
```

### Recipe 2: Lint After Edits

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit",
        "hooks": [
          {
            "type": "command",
            "command": "FILE=$(echo $CLAUDE_TOOL_INPUT | jq -r '.file_path'); if [[ \"$FILE\" == *.py ]]; then ruff check \"$FILE\" --fix; fi"
          }
        ]
      }
    ]
  }
}
```

### Recipe 3: Desktop Notification

```json
{
  "hooks": {
    "Notification": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "notify-send 'Claude Code' \"$CLAUDE_NOTIFICATION_MESSAGE\" 2>/dev/null || osascript -e \"display notification \\\"$CLAUDE_NOTIFICATION_MESSAGE\\\" with title \\\"Claude Code\\\"\" 2>/dev/null"
          }
        ]
      }
    ]
  }
}
```

### Recipe 4: Audit Log for All Tool Calls

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "echo \"$(date -u +%Y-%m-%dT%H:%M:%SZ) | $CLAUDE_TOOL_NAME | $CLAUDE_TOOL_INPUT\" >> /tmp/claude-audit.log"
          }
        ]
      }
    ]
  }
}
```

### Recipe 5: Block Dangerous Commands

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "CMD=$(echo $CLAUDE_TOOL_INPUT | jq -r '.command'); if echo \"$CMD\" | grep -qE 'rm\\s+-rf\\s+/|mkfs|dd\\s+if=|:(){ :|:& };:'; then echo 'Blocked: potentially destructive command' >&2; exit 1; fi"
          }
        ]
      }
    ]
  }
}
```

### Recipe 6: Debug CLAUDE.md Loading

```json
{
  "hooks": {
    "InstructionsLoaded": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "echo \"Instructions loaded at $(date)\" >> /tmp/claude-instructions.log"
          }
        ]
      }
    ]
  }
}
```

---

## Settings Scope

| Scope | File | Applies To |
|-------|------|------------|
| Global | `~/.claude/settings.json` | All projects |
| Project | `.claude/settings.json` | Current project only |
| Enterprise | Managed policy file | All users in organization |

Project-level hooks merge with (not replace) global hooks. Both sets run for matching events.

---

## Debugging Hooks

1. **Test commands manually** before adding them to `settings.json`
2. **Log to a file** using `>> /tmp/hook-debug.log 2>&1` to capture stdout and stderr
3. **Use `InstructionsLoaded`** to verify which CLAUDE.md files Claude sees
4. **Check exit codes** — a non-zero exit in PreToolUse blocks the tool silently if you do not write to stderr

---

## Navigation

| Direction | Link |
|-----------|------|
| Previous | [Module Overview](README.md) |
| Next | [MCP Servers](mcp-servers.md) |
| Module Home | [Module 06 Overview](README.md) |
