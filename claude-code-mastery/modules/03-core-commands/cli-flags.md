# CLI Flags & Options

**Module 03, Lesson 4 — Claude Code Mastery**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Claude Code accepts many command-line flags for controlling behavior, especially in non-interactive (headless) and scripted usage. This is your complete reference.

---

## Complete CLI Flags Reference

### Basic Usage

```bash
claude                          # Start interactive session
claude "your prompt here"       # Start with initial prompt
claude -p "prompt"              # Non-interactive (print mode)
```

### Session Management

| Flag | Description | Example |
|------|-------------|---------|
| `--resume` | Resume a previous session (interactive picker) | `claude --resume` |
| `--resume <id>` | Resume specific session by ID | `claude --resume abc123` |
| `--continue` | Continue the most recent session | `claude --continue` |
| `--from-pr <number>` | Resume session that created a PR | `claude --from-pr 42` |

### Model & Thinking

| Flag | Description | Example |
|------|-------------|---------|
| `--model <name>` | Set the AI model | `claude --model opus` |
| `--model <name>[1m]` | Use 1M context variant | `claude --model sonnet[1m]` |

### Output Control

| Flag | Description | Example |
|------|-------------|---------|
| `-p`, `--print` | Non-interactive mode (print and exit) | `claude -p "explain this code"` |
| `--output-format text` | Plain text output (default for `-p`) | `claude -p --output-format text "..."` |
| `--output-format json` | JSON output | `claude -p --output-format json "..."` |
| `--output-format stream-json` | Streaming JSON (line-delimited) | `claude -p --output-format stream-json "..."` |
| `--verbose` | Show detailed output including thinking | `claude --verbose` |

### Permission Control

| Flag | Description | Example |
|------|-------------|---------|
| `--permission-mode <mode>` | Set permission mode | `claude --permission-mode plan` |
| `--allowedTools <tools>` | Whitelist specific tools | `claude --allowedTools "Bash(npm*),Edit"` |
| `--denyTools <tools>` | Blacklist specific tools | `claude --denyTools "Bash(rm*)"` |
| `--dangerously-skip-permissions` | Skip all permission checks | `claude --dangerously-skip-permissions` |

### System Prompt

| Flag | Description | Example |
|------|-------------|---------|
| `--system-prompt <text>` | Replace system prompt entirely | `claude -p --system-prompt "You are a Go expert" "..."` |
| `--append-system-prompt <text>` | Add to system prompt | `claude -p --append-system-prompt "Always use TypeScript" "..."` |

### Input

| Flag | Description | Example |
|------|-------------|---------|
| `--input-format text` | Input is plain text (default) | `echo "hello" \| claude -p --input-format text` |
| `--input-format stream-json` | Input is streaming JSON | Complex piping scenarios |
| `--max-turns <n>` | Limit agentic turns | `claude -p --max-turns 5 "..."` |

### Git Integration

| Flag | Description | Example |
|------|-------------|---------|
| `--worktree <name>` | Create isolated git worktree | `claude --worktree feature-auth` |
| `--worktree` | Auto-generated worktree name | `claude --worktree` |

### MCP Configuration

| Flag | Description | Example |
|------|-------------|---------|
| `--mcp-config <file>` | Load MCP config from file | `claude --mcp-config mcp.json` |

---

## Non-Interactive (Headless) Mode

### Basic Print Mode

```bash
claude -p "What files are in this directory?"
```

Claude executes the task and prints the result to stdout, then exits.

### Piping Input

```bash
# Pipe file contents
cat error.log | claude -p "What's causing these errors?"

# Pipe command output
git diff | claude -p "Summarize these changes"

# Pipe and save output
cat src/api.ts | claude -p "Add TypeScript types" > src/api-typed.ts
```

### JSON Output

```bash
claude -p --output-format json "List all TODO comments in the codebase"
```

Output structure:
```json
{
  "type": "result",
  "subtype": "success",
  "cost_usd": 0.003,
  "is_error": false,
  "duration_ms": 5234,
  "duration_api_ms": 3200,
  "num_turns": 3,
  "result": "Found 5 TODO comments:\n1. src/auth.ts:23 - TODO: Add rate limiting\n..."
}
```

### Streaming JSON

```bash
claude -p --output-format stream-json "Refactor the auth module"
```

Each line is a JSON object representing a conversation event (assistant message, tool use, tool result, etc.).

### Limiting Turns

```bash
claude -p --max-turns 3 "Find and fix the bug in auth.ts"
```

Limits Claude to 3 agentic turns. Useful for:
- CI/CD pipelines with time constraints
- Simple tasks that shouldn't loop
- Cost control

### Custom System Prompts

```bash
# Replace entire system prompt
claude -p --system-prompt "You are a Python security auditor. Only report vulnerabilities." \
  "Review this code for security issues"

# Append to existing system prompt
claude -p --append-system-prompt "Always respond in JSON format" \
  "List the project dependencies"
```

### Tool Filtering

```bash
# Only allow reading and searching (no editing)
claude -p --allowedTools "Read,Glob,Grep" "Find all API endpoints"

# Block dangerous commands
claude -p --denyTools "Bash(rm*),Bash(sudo*)" "Clean up temp files"

# Allow specific bash patterns
claude -p --allowedTools "Bash(npm test),Bash(npm run*),Read,Edit" "Run tests and fix failures"
```

---

## Scripting Examples

### CI/CD Code Review

```bash
#!/bin/bash
# Automated code review in CI

REVIEW=$(git diff main...HEAD | claude -p \
  --output-format json \
  --max-turns 5 \
  --allowedTools "Read,Glob,Grep" \
  "Review these changes for bugs, security issues, and code quality")

echo "$REVIEW" | jq -r '.result'
```

### Batch File Processing

```bash
#!/bin/bash
# Add TypeScript types to all .js files

for file in src/**/*.js; do
  echo "Processing $file..."
  cat "$file" | claude -p \
    --system-prompt "You are a TypeScript migration expert" \
    "Convert this JavaScript to TypeScript with proper types" \
    > "${file%.js}.ts"
done
```

### Automated Documentation

```bash
#!/bin/bash
# Generate API documentation

claude -p \
  --max-turns 10 \
  --allowedTools "Read,Glob,Grep" \
  "Read all files in src/api/ and generate comprehensive API documentation in Markdown format" \
  > docs/API.md
```

### Multi-Conversation Pipeline

```bash
#!/bin/bash
# Chain multiple Claude sessions

# Step 1: Analyze
ANALYSIS=$(claude -p --output-format json "Analyze the codebase architecture")

# Step 2: Plan
PLAN=$(echo "$ANALYSIS" | jq -r '.result' | claude -p --output-format json \
  "Based on this analysis, create a refactoring plan")

# Step 3: Execute
echo "$PLAN" | jq -r '.result' | claude -p \
  "Execute this refactoring plan step by step"
```

---

## Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `ANTHROPIC_API_KEY` | API key | OAuth token |
| `ANTHROPIC_MODEL` | Default model | `default` |
| `CLAUDE_CODE_EFFORT_LEVEL` | Thinking effort | `medium` |
| `CLAUDE_CONFIG_DIR` | Config directory | `~/.claude` |
| `CLAUDE_CODE_DISABLE_1M_CONTEXT` | Disable 1M context | `0` |
| `CLAUDE_CODE_DISABLE_ADAPTIVE_THINKING` | Disable adaptive reasoning | `0` |
| `MAX_THINKING_TOKENS` | Cap thinking tokens | Model default |
| `ENABLE_TOOL_SEARCH` | Tool search threshold | `auto:5` |
| `CLAUDE_CODE_USE_BEDROCK` | Use AWS Bedrock | `0` |
| `CLAUDE_CODE_USE_VERTEX` | Use Google Vertex | `0` |
| `CLAUDE_CODE_USE_FOUNDRY` | Use MS Foundry | `0` |
| `CLAUDE_CODE_API_KEY_HELPER_TTL_MS` | Key refresh interval | `300000` |

---

**Next:** [Permission Modes Deep Dive](permission-modes.md)

[← Back to Module Overview](README.md)

---

*Module 03, Lesson 4 — Claude Code Mastery — March 2026*
