# Explain Commands

**Module 06, Lesson 2 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

`gh copilot explain` takes any shell command and provides a **clear, detailed explanation** of what it does. This is invaluable when you encounter unfamiliar commands in scripts, documentation, or Stack Overflow answers.

---

## Basic Usage

```bash
gh copilot explain "command to explain"
```

---

## Examples

### Example 1: Complex Find Command

```bash
gh copilot explain "find /var/log -name '*.log' -mtime +30 -exec gzip {} \;"
```

**Copilot explains:**
- `find /var/log` — Search in the /var/log directory
- `-name '*.log'` — Match files ending in .log
- `-mtime +30` — Modified more than 30 days ago
- `-exec gzip {} \;` — Compress each matching file with gzip

### Example 2: Git Command

```bash
gh copilot explain "git rebase -i HEAD~5 --autosquash"
```

**Copilot explains:**
- `git rebase -i` — Interactive rebase
- `HEAD~5` — Last 5 commits
- `--autosquash` — Automatically reorder and squash commits marked with `fixup!` or `squash!`

### Example 3: Docker Command

```bash
gh copilot explain "docker run -d --rm -p 8080:80 -v $(pwd):/app -e NODE_ENV=production --name myapp node:18-alpine"
```

**Copilot explains:**
- `-d` — Run in detached mode (background)
- `--rm` — Remove container when it stops
- `-p 8080:80` — Map port 8080 on host to port 80 in container
- `-v $(pwd):/app` — Mount current directory as /app in container
- `-e NODE_ENV=production` — Set environment variable
- `--name myapp` — Name the container "myapp"
- `node:18-alpine` — Use Node.js 18 on Alpine Linux

### Example 4: Networking Command

```bash
gh copilot explain "netstat -tlnp | grep :3000"
```

### Example 5: Kubernetes Command

```bash
gh copilot explain "kubectl get pods -n production -o jsonpath='{.items[*].metadata.name}' --field-selector=status.phase!=Running"
```

### Example 6: AWK One-Liner

```bash
gh copilot explain "awk -F',' '{sum+=$3} END {printf \"Average: %.2f\n\", sum/NR}' data.csv"
```

---

## Interactive Mode

If you run `gh copilot explain` without a command, it enters **interactive mode**:

```bash
gh copilot explain
# Copilot prompts: "What command would you like me to explain?"
# You type the command
# Copilot provides the explanation
```

---

## Tips for Using Explain

1. **Quote the command** — Always wrap the command in quotes to prevent shell interpretation
2. **Include the full command** — Provide flags, arguments, and pipes for a complete explanation
3. **Use for learning** — Great for understanding commands in CI/CD pipelines, Dockerfiles, and Makefiles
4. **Pipe chains welcome** — Multi-command pipes are explained step by step

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 06: Copilot CLI](README.md) |
| Previous Lesson | [Installation](installation.md) |
| Next Lesson | [Suggest Commands](suggest-commands.md) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
