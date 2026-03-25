# Complete Command Reference

**Module 11, Lesson 1 — Claude Code Mastery**

**Instructor: Jabbir Basha, Principal AI Engineer**

---

## 1. Slash Commands

All slash commands are typed directly in the Claude Code interactive prompt.

| Command | Description |
|---------|-------------|
| `/bug` | Report a bug to the Claude Code team |
| `/clear` | Clear conversation history and free up context window |
| `/compact` | Condense the conversation to save context space; optionally pass a focus topic |
| `/config` | Open or display configuration settings |
| `/cost` | Show token usage and estimated cost for the current session |
| `/doctor` | Run diagnostic checks on your Claude Code installation |
| `/help` | Show available slash commands and brief usage info |
| `/init` | Generate a CLAUDE.md file for the current project based on codebase analysis |
| `/login` | Authenticate with your Anthropic account or API key |
| `/logout` | Sign out of the current authentication session |
| `/memory` | View or edit the project CLAUDE.md memory file |
| `/model` | Switch the active model (e.g., `claude-sonnet-4-20250514`) |
| `/permissions` | View or modify tool permission rules for the current session |
| `/pr-review` | Review a pull request (pass PR number or URL) |
| `/review` | Request a code review of staged or recent changes |
| `/status` | Show current session status: model, permissions, cost, context usage |
| `/terminal-setup` | Configure terminal integration (shell, iTerm2, etc.) |
| `/vim` | Toggle Vim keybinding mode for the input area |

---

## 2. CLI Flags

Flags passed when launching `claude` from the terminal.

| Flag | Short | Description |
|------|-------|-------------|
| `--allowedTools` | | Comma-separated list of tools to allow (e.g., `Bash,Read,Write`) |
| `--append-system-prompt` | | Append text to the system prompt |
| `--chat` | `-c` | Start in interactive chat mode (default) |
| `--continue` | `-r` | Resume the most recent conversation |
| `--dangerously-skip-permissions` | | Skip all permission checks (use with caution) |
| `--help` | `-h` | Show help text and exit |
| `--input-format` | | Set input format: `text` (default), `stream-json` |
| `--json` | | Output responses in JSON format |
| `--max-turns` | | Maximum number of agentic turns before stopping |
| `--model` | `-m` | Specify the model to use (e.g., `claude-sonnet-4-20250514`) |
| `--no-cache` | | Disable prompt caching |
| `--output-format` | | Set output format: `text` (default), `json`, `stream-json` |
| `--permission-mode` | | Set permission mode: `default`, `plan`, `auto-edit`, `full-auto` |
| `--permission-prompt-tool` | | MCP tool to use for permission prompts |
| `--print` | `-p` | Non-interactive mode: print response and exit |
| `--resume` | | Resume a specific session by ID |
| `--system-prompt` | | Override the entire system prompt |
| `--verbose` | `-v` | Enable verbose logging output |
| `--version` | | Print the installed version and exit |

### Usage Patterns

```bash
# One-shot mode
claude -p "Explain this function" < file.py

# Pipe input
cat error.log | claude -p "What is wrong?"

# Resume last session
claude --continue

# Full auto for CI
claude -p --permission-mode full-auto "Run tests and fix failures"

# Specify model
claude -m claude-sonnet-4-20250514 -p "Quick question"

# Limit agentic turns
claude --max-turns 5 -p "Refactor this module"
```

---

## 3. Built-in Tools

Tools are the actions Claude Code can take on your behalf.

| Tool | Description |
|------|-------------|
| `Read` | Read file contents from disk. Supports text files, images, PDFs, and notebooks. |
| `Write` | Create a new file or completely overwrite an existing file. |
| `Edit` | Make targeted string replacements in an existing file. |
| `Bash` | Execute a shell command and return its output. |
| `Glob` | Search for files by name pattern (e.g., `**/*.ts`). |
| `Grep` | Search file contents using regex patterns (powered by ripgrep). |
| `WebFetch` | Fetch content from a URL (web pages, APIs). |
| `WebSearch` | Search the web for information. |
| `TodoWrite` | Manage an internal task list for multi-step operations. |
| `NotebookEdit` | Edit Jupyter notebook cells. |
| `Agent` | Spawn a sub-agent for complex multi-step research tasks. |

---

## 4. Permission Modes

| Mode | Description | Tool Behavior |
|------|-------------|---------------|
| `default` | Standard interactive mode | Asks before file writes, edits, and most bash commands |
| `plan` | Read-only planning mode | Claude can read and search but cannot write, edit, or execute |
| `auto-edit` | Auto-approve file changes | File writes and edits are auto-approved; bash still requires approval |
| `full-auto` | Approve everything | All tool calls are auto-approved; use only in trusted/sandboxed environments |

### Permission Rules in Settings

```json
{
  "permissions": {
    "allow": [
      "Bash(npm test)",
      "Bash(npm run lint)",
      "Read",
      "Glob",
      "Grep"
    ],
    "deny": [
      "Bash(rm -rf *)",
      "Bash(git push --force)"
    ]
  }
}
```

**Rule syntax:** `ToolName` allows the entire tool. `ToolName(pattern)` allows only commands matching the pattern. Patterns support glob-style matching.

---

## 5. Environment Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `ANTHROPIC_API_KEY` | API key for direct Anthropic API access | `sk-ant-...` |
| `ANTHROPIC_MODEL` | Default model override | `claude-sonnet-4-20250514` |
| `CLAUDE_CODE_USE_BEDROCK` | Use AWS Bedrock as the provider | `1` |
| `CLAUDE_CODE_USE_VERTEX` | Use Google Vertex AI as the provider | `1` |
| `AWS_REGION` | AWS region for Bedrock | `us-east-1` |
| `AWS_ACCESS_KEY_ID` | AWS access key for Bedrock authentication | `AKIA...` |
| `AWS_SECRET_ACCESS_KEY` | AWS secret key for Bedrock authentication | `wJal...` |
| `AWS_SESSION_TOKEN` | AWS session token (temporary credentials) | `FwoG...` |
| `CLOUD_ML_REGION` | Google Cloud region for Vertex AI | `us-central1` |
| `ANTHROPIC_VERTEX_PROJECT_ID` | Google Cloud project ID for Vertex AI | `my-project-123` |
| `CLAUDE_CODE_MAX_OUTPUT_TOKENS` | Override max output tokens per response | `16384` |
| `CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC` | Disable telemetry and non-essential network calls | `1` |
| `CLAUDE_CODE_SKIP_DOCTOR` | Skip startup diagnostic checks | `1` |
| `HTTP_PROXY` | HTTP proxy URL | `http://proxy:8080` |
| `HTTPS_PROXY` | HTTPS proxy URL | `https://proxy:8443` |
| `NO_PROXY` | Comma-separated list of hosts to bypass proxy | `localhost,127.0.0.1` |
| `CLAUDE_CODE_API_KEY_HELPER_TTL_MS` | Cache TTL for API key helper results (ms) | `60000` |
| `CLAUDE_CODE_CONFIG_DIR` | Override the default config directory path | `~/.config/claude-code` |

---

## 6. Settings (settings.json)

Settings can be configured at three levels: user (`~/.claude/settings.json`), project (`.claude/settings.json`), and enterprise (`/etc/claude/settings.json` or managed policy).

| Key | Type | Description |
|-----|------|-------------|
| `permissions.allow` | `string[]` | List of tool permission rules to auto-allow |
| `permissions.deny` | `string[]` | List of tool permission rules to always deny |
| `env` | `object` | Environment variables to set for Claude Code sessions |
| `hooks` | `object` | Hook definitions (see Hooks section below) |
| `model` | `string` | Default model to use |
| `small_fast_model` | `string` | Model to use for background/fast tasks (e.g., compact) |
| `temperature` | `number` | Sampling temperature override |
| `verbose` | `boolean` | Enable verbose output by default |
| `apiKeyHelper` | `string` | Shell command to dynamically retrieve API keys |
| `preferredNotifChannel` | `string` | Notification channel: `iterm2`, `terminal_bell`, `iterm2_with_bell` |
| `theme` | `string` | Color theme for the TUI |
| `terminal_emulator` | `string` | Terminal emulator identifier for integration features |
| `projects` | `object` | Per-project settings keyed by project path |
| `mcpServers` | `object` | MCP server configurations |
| `autoUpdaterStatus` | `string` | Auto-updater preference: `enabled`, `disabled` |
| `releaseChannel` | `string` | Update channel: `stable`, `beta` |

### Example settings.json

```json
{
  "model": "claude-sonnet-4-20250514",
  "permissions": {
    "allow": [
      "Read",
      "Glob",
      "Grep",
      "Bash(npm test)",
      "Bash(npm run *)"
    ],
    "deny": [
      "Bash(rm -rf /)",
      "Bash(git push --force)"
    ]
  },
  "env": {
    "NODE_ENV": "development"
  },
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"]
    }
  }
}
```

---

## 7. CLAUDE.md Scopes

CLAUDE.md files provide persistent instructions. Scope determines where Claude looks for them.

| Scope | Location | Loaded When | Use Case |
|-------|----------|-------------|----------|
| **User-global** | `~/.claude/CLAUDE.md` | Always | Personal preferences, coding style, global rules |
| **Project root** | `./CLAUDE.md` | When working in that project | Project conventions, architecture notes, tech stack |
| **Project config** | `./.claude/CLAUDE.md` | When working in that project | Same as project root (alternative location) |
| **Directory-local** | `any-dir/CLAUDE.md` | When Claude reads files in that directory | Module-specific rules, directory-level context |
| **Parent directories** | `../CLAUDE.md`, `../../CLAUDE.md` | Traversed up to filesystem root | Monorepo or workspace-level conventions |
| **Enterprise** | Managed policy `CLAUDE.md` | Always (if configured) | Organization-wide rules and compliance requirements |

### Scope Precedence (highest to lowest)

1. Enterprise managed policy CLAUDE.md
2. Directory-local CLAUDE.md (nearest to the files being edited)
3. Project root CLAUDE.md / .claude/CLAUDE.md
4. Parent directory CLAUDE.md files
5. User-global ~/.claude/CLAUDE.md

---

## 8. Hook Types

Hooks let you run custom scripts at specific points in Claude Code's workflow.

| Hook | Trigger | Common Use Cases |
|------|---------|-----------------|
| `PreToolUse` | Before a tool is executed | Validate commands, block dangerous operations, add logging |
| `PostToolUse` | After a tool finishes executing | Format output, run linters after edits, post-processing |
| `Notification` | When Claude sends a notification | Custom notification routing, Slack alerts, desktop popups |
| `Stop` | When Claude finishes its response | Auto-run tests, commit checks, summary generation |

### Hook Configuration Structure

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          {
            "type": "command",
            "command": "python3 /path/to/validate.py \"$TOOL_INPUT\""
          }
        ]
      }
    ],
    "PostToolUse": [
      {
        "matcher": "Write|Edit",
        "hooks": [
          {
            "type": "command",
            "command": "npx prettier --write \"$TOOL_INPUT_FILE_PATH\""
          }
        ]
      }
    ],
    "Stop": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "echo 'Claude finished a response' | notify-send"
          }
        ]
      }
    ]
  }
}
```

### Hook Exit Codes

| Exit Code | Meaning |
|-----------|---------|
| `0` | Proceed normally |
| `2` | Block the tool call (PreToolUse only) — Claude is told the action was denied |
| Any other | Hook failed; error is reported but tool execution continues |

---

## 9. Model Aliases

| Alias | Resolves To | Notes |
|-------|-------------|-------|
| `claude-sonnet-4-20250514` | Claude Sonnet 4 (May 2025) | Balanced speed and capability |
| `claude-opus-4-20250514` | Claude Opus 4 (May 2025) | Most capable, highest cost |
| `claude-haiku-3-5-20241022` | Claude 3.5 Haiku (Oct 2024) | Fastest, lowest cost |
| `sonnet` | Latest Claude Sonnet | Convenience alias |
| `opus` | Latest Claude Opus | Convenience alias |
| `haiku` | Latest Claude Haiku | Convenience alias |

Switch models at any time:

```
/model sonnet
/model opus
/model claude-sonnet-4-20250514
```

Or set a default:

```bash
# Via environment variable
export ANTHROPIC_MODEL=claude-sonnet-4-20250514

# Via CLI flag
claude -m opus

# Via settings.json
{"model": "claude-sonnet-4-20250514"}
```

---

## 10. MCP Server Configuration

MCP (Model Context Protocol) servers extend Claude Code with additional tools.

```json
{
  "mcpServers": {
    "server-name": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-name"],
      "env": {
        "API_TOKEN": "your-token"
      },
      "cwd": "/optional/working/directory"
    }
  }
}
```

| Field | Required | Description |
|-------|----------|-------------|
| `command` | Yes | Executable to launch the server |
| `args` | Yes | Arguments to pass to the command |
| `env` | No | Environment variables for the server process |
| `cwd` | No | Working directory for the server process |

MCP servers can be defined in:
- User settings: `~/.claude/settings.json`
- Project settings: `.claude/settings.json`

---

## 11. Quick Reference: Common Workflows

### Start a New Project
```bash
cd my-project
claude
> /init
```

### Fix a Bug
```bash
claude -p "There is a bug where X happens instead of Y. Find and fix it."
```

### Code Review
```bash
claude
> /review
# Or review a specific PR
> /pr-review 42
```

### Run in CI/CD
```bash
claude -p --permission-mode full-auto \
  --max-turns 10 \
  "Run the test suite, fix any failures, and report results"
```

### Context Running Low
```
/compact focus on the authentication module
```

### Switch Provider to Bedrock
```bash
export CLAUDE_CODE_USE_BEDROCK=1
export AWS_REGION=us-east-1
claude
```

### Switch Provider to Vertex AI
```bash
export CLAUDE_CODE_USE_VERTEX=1
export CLOUD_ML_REGION=us-central1
export ANTHROPIC_VERTEX_PROJECT_ID=my-project
claude
```

---

## Navigation

| Direction | Link |
|-----------|------|
| Previous Lesson | [Module 11 Overview](README.md) |
| Next Lesson | [Keyboard Shortcuts Reference](keyboard-shortcuts-reference.md) |
| Module Overview | [Module 11: Cheat Sheets](README.md) |

---

> **Tip:** Search this file with Ctrl+F (or `/` in Vim mode) to find any command, flag, or setting instantly.
