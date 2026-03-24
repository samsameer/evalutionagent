# Copilot CLI Installation

**Module 02, Lesson 4 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

GitHub Copilot CLI brings AI assistance directly to your terminal. It can explain complex commands, suggest the right command for a task, and help you navigate Git and the GitHub CLI. This lesson covers installation and initial setup.

---

## Prerequisites

- **GitHub CLI (`gh`)** version 2.40.0 or later
- A GitHub account with **Copilot Pro, Pro+, Business, or Enterprise** (CLI is not available on the Free tier)
- A terminal (bash, zsh, PowerShell, or fish)

---

## Step 1: Install GitHub CLI

If you do not have the GitHub CLI installed:

### macOS
```bash
brew install gh
```

### Windows
```powershell
winget install --id GitHub.cli
```

### Linux (Debian/Ubuntu)
```bash
sudo apt install gh
```

### Linux (Fedora)
```bash
sudo dnf install gh
```

Verify installation:
```bash
gh --version
```

---

## Step 2: Authenticate GitHub CLI

```bash
gh auth login
```

Follow the prompts to authenticate with your GitHub account. Choose HTTPS and authenticate via browser.

---

## Step 3: Install the Copilot CLI Extension

```bash
gh extension install github/gh-copilot
```

Verify installation:
```bash
gh copilot --version
```

---

## Step 4: Test Copilot CLI

### Test `explain`:
```bash
gh copilot explain "find . -name '*.log' -mtime +30 -delete"
```

Expected output: A clear, detailed explanation of what the command does — finds and deletes log files older than 30 days.

### Test `suggest`:
```bash
gh copilot suggest "list all docker containers sorted by size"
```

Expected output: A suggested shell command like `docker ps -a --size --format "table {{.Names}}\t{{.Size}}" | sort -k2 -h`

---

## Step 5: Configure Shell Aliases (Optional)

For faster access, add aliases to your shell configuration:

### bash/zsh (~/.bashrc or ~/.zshrc)
```bash
alias explain='gh copilot explain'
alias suggest='gh copilot suggest'
```

### PowerShell ($PROFILE)
```powershell
Set-Alias explain 'gh copilot explain'
Set-Alias suggest 'gh copilot suggest'
```

After adding aliases, reload your shell:
```bash
source ~/.bashrc  # or ~/.zshrc
```

Now you can simply type:
```bash
explain "awk '{print $1}' access.log | sort | uniq -c | sort -rn | head -10"
suggest "compress all PNG files in this directory"
```

---

## Verification Checklist

- [ ] GitHub CLI (`gh`) is installed and up to date
- [ ] You are authenticated with `gh auth login`
- [ ] Copilot CLI extension is installed
- [ ] `gh copilot explain` works and returns explanations
- [ ] `gh copilot suggest` works and suggests commands

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 02: Setup & Installation](README.md) |
| Previous Lesson | [Neovim & Xcode Setup](neovim-xcode-setup.md) |
| Next Module | [Module 03: VS Code Core Features](../03-vs-code-core/) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
