# Installation Guide

**Module 02, Lesson 2 — Claude Code Mastery**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Claude Code is distributed as an npm package. Installation takes about 2 minutes on any platform.

---

## Install on macOS

### Step 1: Verify Node.js

```bash
node --version
# Must be v18.0.0 or higher
```

If not installed, use Homebrew:

```bash
brew install node
```

### Step 2: Install Claude Code

```bash
npm install -g @anthropic-ai/claude-code
```

### Step 3: Verify Installation

```bash
claude --version
# Should show: claude-code v2.8.x
```

### Step 4: Launch

```bash
claude
```

---

## Install on Linux

### Step 1: Install Node.js

**Ubuntu/Debian:**
```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt-get install -y nodejs
```

**Fedora/RHEL:**
```bash
curl -fsSL https://rpm.nodesource.com/setup_20.x | sudo bash -
sudo dnf install -y nodejs
```

**Using nvm (recommended):**
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
source ~/.bashrc
nvm install 20
nvm use 20
```

### Step 2: Install Claude Code

```bash
npm install -g @anthropic-ai/claude-code
```

### Step 3: Verify and Launch

```bash
claude --version
claude
```

---

## Install on Windows (WSL)

Claude Code runs on Windows through **Windows Subsystem for Linux (WSL)**.

### Step 1: Install WSL

Open PowerShell as Administrator:

```powershell
wsl --install
```

Restart your computer, then open the Ubuntu terminal.

### Step 2: Install Node.js in WSL

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
source ~/.bashrc
nvm install 20
nvm use 20
```

### Step 3: Install Claude Code

```bash
npm install -g @anthropic-ai/claude-code
```

### Step 4: Launch

```bash
claude
```

> **Note:** Claude Code works with your WSL filesystem. Navigate to your project directory (`/home/username/projects/`) rather than `/mnt/c/` for best performance.

---

## Update Claude Code

```bash
npm update -g @anthropic-ai/claude-code
```

Check current version:
```bash
claude --version
```

---

## Uninstall Claude Code

```bash
npm uninstall -g @anthropic-ai/claude-code
```

To remove all local data:
```bash
rm -rf ~/.claude
rm -f ~/.claude.json
```

---

## Troubleshooting Installation

### Permission Errors on npm

If you get `EACCES` permission errors:

```bash
# Option 1: Use nvm (recommended)
nvm install 20 && nvm use 20

# Option 2: Fix npm permissions
mkdir ~/.npm-global
npm config set prefix '~/.npm-global'
echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
npm install -g @anthropic-ai/claude-code
```

### Node Version Too Old

```bash
node --version
# If below v18, upgrade:
nvm install 20
nvm use 20
```

### Command Not Found After Install

```bash
# Check where npm installed it
npm list -g @anthropic-ai/claude-code

# Make sure npm global bin is in PATH
echo 'export PATH=$(npm prefix -g)/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```

### Run Doctor

After installation, use the built-in diagnostics:

```bash
claude
# Then inside Claude Code:
/doctor
```

This checks your installation, authentication, and configuration.

---

**Next:** [Authentication & Login](authentication.md)

[← Back to Module Overview](README.md)

---

*Module 02, Lesson 2 — Claude Code Mastery — March 2026*
