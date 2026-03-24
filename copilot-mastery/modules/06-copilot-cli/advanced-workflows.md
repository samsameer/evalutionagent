# Advanced CLI Workflows

**Module 06, Lesson 4 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

This lesson combines Copilot CLI commands into real-world workflows that save significant time in daily development, DevOps, and system administration tasks.

---

## Workflow 1: Debugging a Production Issue

```bash
# Step 1: Find recent error logs
gh copilot suggest "show the last 50 lines of error log containing 'TimeoutException'"

# Step 2: Understand the error
gh copilot explain "grep -A5 'TimeoutException' /var/log/app/error.log | tail -50"

# Step 3: Check if it's a known issue
gh copilot suggest "search GitHub issues for TimeoutException in this repo"

# Step 4: Find the commit that might have caused it
gh copilot suggest "show git log for last week with files changed"
```

---

## Workflow 2: Setting Up a New Server

```bash
# Each step: describe what you need, get the command
gh copilot suggest "update all packages on Ubuntu"
gh copilot suggest "install Node.js 20 LTS on Ubuntu"
gh copilot suggest "configure nginx as reverse proxy for port 3000"
gh copilot suggest "generate an SSL certificate with Let's Encrypt for mysite.com"
gh copilot suggest "set up automatic security updates on Ubuntu"
```

---

## Workflow 3: Git Archaeology

```bash
# Find when a function was added
gh copilot suggest "find the commit that first added the function processPayment"

# Find who changed a specific line
gh copilot suggest "show git blame for line 42 of src/payment.ts"

# Find all commits touching a file
gh copilot suggest "show commit history for src/auth/login.ts with diffs"

# Find commits between two tags
gh copilot suggest "list all commits between v2.0 and v3.0 that mention 'fix'"
```

---

## Workflow 4: Docker Management

```bash
gh copilot suggest "remove all stopped containers and unused images"
gh copilot suggest "show logs of a container from the last 30 minutes"
gh copilot suggest "copy a file from a running container to local filesystem"
gh copilot suggest "inspect the network settings of a running container"
```

---

## Shell Integration with Aliases

For maximum efficiency, set up these aliases:

```bash
# ~/.bashrc or ~/.zshrc
alias '??'='gh copilot suggest'
alias '?!'='gh copilot explain'
```

Now you can:
```bash
?? "find all TODO comments in TypeScript files"
?! "tar -czf backup.tar.gz --exclude=node_modules ."
```

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 06: Copilot CLI](README.md) |
| Previous Lesson | [Suggest Commands](suggest-commands.md) |
| Next Module | [Module 07: Copilot on GitHub.com](../07-github-dot-com/) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
