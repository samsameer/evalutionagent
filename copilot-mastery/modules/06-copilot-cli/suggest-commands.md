# Suggest Commands

**Module 06, Lesson 3 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

`gh copilot suggest` generates the right command for any task described in natural language. It supports three categories: **shell commands**, **Git commands**, and **GitHub CLI commands**.

---

## Basic Usage

```bash
gh copilot suggest "description of what you want to do"
```

Copilot will:
1. Ask which type of command you need (generic shell, git, or gh)
2. Generate the appropriate command
3. Let you copy, run, or revise it

---

## Command Types

### Generic Shell Commands

```bash
gh copilot suggest "find all Python files larger than 1MB"
# Suggests: find . -name "*.py" -size +1M

gh copilot suggest "compress all JPG files in current directory to a zip"
# Suggests: zip images.zip *.jpg

gh copilot suggest "show disk usage of top 10 largest directories"
# Suggests: du -h --max-depth=1 | sort -hr | head -10

gh copilot suggest "kill all processes listening on port 3000"
# Suggests: lsof -ti:3000 | xargs kill -9

gh copilot suggest "monitor CPU and memory usage in real time"
# Suggests: top -o %CPU

gh copilot suggest "recursively change permissions of all directories to 755 and files to 644"
# Suggests: find . -type d -exec chmod 755 {} + && find . -type f -exec chmod 644 {} +
```

### Git Commands

```bash
gh copilot suggest "undo the last commit but keep the changes"
# Suggests: git reset --soft HEAD~1

gh copilot suggest "show all branches that have been merged into main"
# Suggests: git branch --merged main

gh copilot suggest "find which commit introduced a bug between v1.0 and v2.0"
# Suggests: git bisect start v2.0 v1.0

gh copilot suggest "squash the last 3 commits into one"
# Suggests: git rebase -i HEAD~3

gh copilot suggest "show the diff of a specific file between two branches"
# Suggests: git diff main..feature-branch -- path/to/file.ts

gh copilot suggest "create a patch file from the last commit"
# Suggests: git format-patch -1 HEAD
```

### GitHub CLI Commands

```bash
gh copilot suggest "create a pull request from current branch"
# Suggests: gh pr create --fill

gh copilot suggest "list all open issues assigned to me"
# Suggests: gh issue list --assignee @me --state open

gh copilot suggest "download the latest release artifact"
# Suggests: gh release download --pattern '*.tar.gz'

gh copilot suggest "check the status of CI checks on my PR"
# Suggests: gh pr checks

gh copilot suggest "review a pull request in the terminal"
# Suggests: gh pr review --comment
```

---

## After Suggestion: Your Options

When Copilot suggests a command, you have three options:

| Option | Description |
|--------|-------------|
| **Copy to clipboard** | Copy the command for manual execution |
| **Execute** | Run the command immediately |
| **Revise** | Modify your description for a different suggestion |

---

## Real-World Workflow Examples

### DevOps Workflow
```bash
suggest "check which containers are using the most memory"
suggest "view the last 100 lines of nginx error log"
suggest "create a cron job that runs backup.sh every day at 2am"
suggest "set up a firewall rule to allow only SSH and HTTP"
```

### Database Workflow
```bash
suggest "dump a PostgreSQL database to a file"
suggest "import a SQL file into MySQL"
suggest "show the size of all tables in a PostgreSQL database"
```

### Development Workflow
```bash
suggest "watch for file changes and restart the Node.js server"
suggest "run ESLint on all TypeScript files and auto-fix issues"
suggest "generate a dependency graph for this project"
```

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 06: Copilot CLI](README.md) |
| Previous Lesson | [Explain Commands](explain-commands.md) |
| Next Lesson | [Advanced CLI Workflows](advanced-workflows.md) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
