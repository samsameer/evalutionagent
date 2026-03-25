# Permission Modes Deep Dive

**Module 03, Lesson 5 — Claude Code Mastery**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Permission modes control how much autonomy Claude Code has. Understanding these modes is critical for both productivity and safety.

---

## The Six Permission Modes

### 1. `default` — Prompt for Everything

```
Prompts for: File edits, bash commands, web requests, MCP tools
Best for: Getting started, sensitive codebases
```

Claude asks before every action. Safest mode.

### 2. `acceptEdits` — Auto-approve File Edits

```
Auto-approves: File edits (Read, Edit, Write)
Prompts for: Bash commands, web requests, MCP tools
Best for: Iterating on code you're reviewing
```

Claude can freely edit your files but still asks before running commands.

### 3. `plan` — Read-Only Analysis

```
Auto-approves: File reads, code search, read-only commands
Blocks: File edits, destructive commands
Best for: Exploring codebases, planning refactors
```

Claude creates a plan you review before any changes are made. When the plan is ready, you can:
- Approve and switch to auto mode for execution
- Approve and accept edits (acceptEdits mode)
- Approve and manually review each change
- Request refinements

### 4. `auto` — Background Safety Classifier (Team/Enterprise)

```
Auto-approves: Local file operations, dependency installs, read-only requests
Classifier checks: External requests, infrastructure changes, production operations
Blocks: Dangerous patterns (curl|bash, force push to main, IAM changes)
Best for: Long-running tasks, reducing prompt fatigue
```

**Requires:** Team or Enterprise plan

**How the classifier works:**
1. Actions matching explicit allow/deny rules resolve immediately
2. Read-only actions and file edits auto-approve
3. Everything else goes to a background safety classifier
4. Classifier blocks if the action looks dangerous

**What gets blocked by default:**
- Downloading and executing code (`curl | bash`)
- Sending sensitive data to external endpoints
- Production deploys and database migrations
- Mass deletion on cloud storage
- Granting IAM or repo permissions
- Force push to `main`/`master`

**What's allowed by default:**
- Local file operations in working directory
- Installing dependencies listed in lock files
- Reading .env and sending credentials to matching APIs
- Read-only HTTP requests
- Pushing to current branch

### 5. `bypassPermissions` — Skip All Checks

```
Auto-approves: EVERYTHING
Best for: Isolated containers, VMs, devcontainers without internet
```

> **Warning:** Offers NO protection against prompt injection. Only use in fully isolated environments.

### 6. `dontAsk` — Pre-approved Tools Only

```
Auto-approves: Only tools matching explicit allow rules
Auto-denies: Everything else
Best for: CI/CD pipelines, locked-down automation
```

---

## Switching Modes

### During a Session

Press `Shift+Tab` to cycle through available modes:

```
default → acceptEdits → plan → [auto] → [bypassPermissions] → default
```

> **Note:** `auto` only appears if enabled (Team/Enterprise). `bypassPermissions` only appears if explicitly enabled.

### At Startup

```bash
claude --permission-mode plan
claude --permission-mode acceptEdits
claude --dangerously-skip-permissions    # bypassPermissions
```

### As Default in Settings

Add to `~/.claude/settings.json`:

```json
{
  "permissions": {
    "defaultMode": "acceptEdits"
  }
}
```

---

## Tool-Specific Permissions

### Allow Rules

```json
{
  "permissions": {
    "allow": [
      "Bash(npm test)",
      "Bash(npm run *)",
      "Bash(git *)",
      "Edit(src/**/*.ts)",
      "Read",
      "Glob",
      "Grep",
      "WebFetch"
    ]
  }
}
```

### Deny Rules

```json
{
  "permissions": {
    "deny": [
      "Bash(rm *)",
      "Bash(sudo *)",
      "Bash(chmod *)",
      "Edit(.env)",
      "Edit(*.key)",
      "Edit(*.pem)"
    ]
  }
}
```

### Pattern Syntax

| Pattern | Matches |
|---------|---------|
| `Bash(*)` | Any bash command |
| `Bash(npm*)` | Commands starting with "npm" |
| `Bash(npm test)` | Exact command "npm test" |
| `Edit(*.md)` | Markdown file edits |
| `Edit(src/**/*.ts)` | TypeScript files in src/ |
| `Read` | All file reads |
| `WebFetch` | Any web fetch |
| `mcp__github__*` | All GitHub MCP tools |
| `Agent` | Subagent spawning |

### Priority

1. **Deny rules** are checked first
2. **Allow rules** are checked second
3. **Permission mode** applies last

---

## Settings File Locations

| File | Scope | Shared |
|------|-------|--------|
| `.claude/settings.json` | Project (committed to git) | Yes, with team |
| `.claude/settings.local.json` | Project (gitignored) | No |
| `~/.claude/settings.json` | User (all projects) | No |
| Managed policy | Organization (IT-managed) | Yes, with org |

### Precedence (highest to lowest)

1. Managed policy (enterprise)
2. Project `.claude/settings.json`
3. Project `.claude/settings.local.json`
4. User `~/.claude/settings.json`

---

## Auto Mode Configuration (Team/Enterprise)

### View Defaults

```bash
claude auto-mode defaults
```

### Trust Specific Infrastructure

```json
{
  "autoMode": {
    "environment": {
      "trustedRepos": [
        "github.com/myorg/*"
      ],
      "trustedCloudBuckets": [
        "s3://my-company-bucket"
      ]
    }
  }
}
```

### Classifier Behavior

If the classifier blocks an action **3 times in a row** or **20 times total** in a session:
- Auto mode pauses
- User is prompted for the action
- Counters reset after approval

---

## Practical Permission Recipes

### Solo Developer (Maximum Productivity)

```json
{
  "permissions": {
    "defaultMode": "acceptEdits",
    "allow": [
      "Bash(npm *)",
      "Bash(git *)",
      "Bash(python *)",
      "Bash(make *)",
      "WebFetch",
      "WebSearch"
    ],
    "deny": [
      "Bash(rm -rf *)",
      "Bash(sudo *)"
    ]
  }
}
```

### Team Environment (Balanced)

```json
{
  "permissions": {
    "defaultMode": "default",
    "allow": [
      "Bash(npm test)",
      "Bash(npm run lint)",
      "Bash(npm run build)",
      "Bash(git status)",
      "Bash(git diff*)",
      "Bash(git log*)",
      "Read",
      "Glob",
      "Grep"
    ],
    "deny": [
      "Bash(git push*)",
      "Bash(npm publish*)",
      "Bash(rm *)",
      "Edit(.env*)",
      "Edit(*.secret*)"
    ]
  }
}
```

### CI/CD Pipeline (Locked Down)

```json
{
  "permissions": {
    "defaultMode": "dontAsk",
    "allow": [
      "Read",
      "Glob",
      "Grep",
      "Bash(npm test)",
      "Bash(npm run build)"
    ]
  }
}
```

---

**Next Module:** [The Memory System (CLAUDE.md) →](../04-memory-system/)

[← Back to Module Overview](README.md) | [Course Home](../../README.md)

---

*Module 03, Lesson 5 — Claude Code Mastery — March 2026*
