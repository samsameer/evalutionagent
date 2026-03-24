# VS Code Setup

**Module 02, Lesson 1 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Visual Studio Code is the **primary and most feature-rich** environment for GitHub Copilot. This lesson covers installing the extensions, authenticating, configuring settings, and verifying everything works.

---

## Step 1: Install VS Code

If you do not already have VS Code installed:

1. Visit [code.visualstudio.com](https://code.visualstudio.com/)
2. Download the installer for your operating system (macOS, Windows, or Linux)
3. Install and launch VS Code

> **Minimum Version:** VS Code 1.95 or later is recommended for all Copilot features including agent mode and NES.

---

## Step 2: Install the GitHub Copilot Extension

There are **two extensions** you should install:

### Extension 1: GitHub Copilot

This is the **core extension** that provides inline code completions (ghost text).

1. Open VS Code
2. Press `Ctrl+Shift+X` (Windows/Linux) or `Cmd+Shift+X` (macOS) to open Extensions
3. Search for **"GitHub Copilot"**
4. Click **Install** on the extension by **GitHub**
5. Wait for installation to complete

### Extension 2: GitHub Copilot Chat

This extension adds **Copilot Chat** — the conversational AI interface.

1. In the Extensions panel, search for **"GitHub Copilot Chat"**
2. Click **Install** on the extension by **GitHub**

> **Note (March 2026):** In the latest VS Code versions, installing "GitHub Copilot" may automatically include Copilot Chat as well. Check if Chat is already available before installing separately.

---

## Step 3: Authenticate with GitHub

After installing the extensions:

1. You will see a **"Sign in to GitHub"** prompt in the bottom-right corner
2. Click the prompt (or click the Copilot icon in the status bar)
3. A browser window will open asking you to authorize VS Code
4. Sign in with your GitHub account
5. Click **"Authorize Visual Studio Code"**
6. Return to VS Code — you should see the Copilot icon active in the status bar

### Status Bar Indicators

| Icon State | Meaning |
|-----------|---------|
| Copilot icon (solid) | Copilot is active and ready |
| Copilot icon (spinning) | Copilot is generating a suggestion |
| Copilot icon (warning) | Authentication issue or subscription problem |
| Copilot icon (disabled) | Copilot is disabled for this file type or globally |

---

## Step 4: Verify Copilot Is Working

1. Create a new file: `test.js` (or any language you prefer)
2. Type the following comment:

```javascript
// Function to calculate the factorial of a number
function factorial(
```

3. Pause after typing the opening parenthesis
4. You should see **ghost text** appear suggesting the parameter and function body
5. Press **Tab** to accept the suggestion

If you see ghost text suggestions, **Copilot is working!**

---

## Step 5: Configure Copilot Settings

Open VS Code settings (`Ctrl+,` or `Cmd+,`) and search for "Copilot" to customize:

### Essential Settings

| Setting | Default | Recommended | Description |
|---------|---------|-------------|-------------|
| `github.copilot.enable` | `true` | `true` | Enable/disable Copilot globally |
| `github.copilot.editor.enableAutoCompletions` | `true` | `true` | Show inline suggestions automatically |
| `editor.inlineSuggest.enabled` | `true` | `true` | Enable inline suggestion rendering |
| `github.copilot.chat.localeOverride` | `auto` | Your locale | Language for chat responses |

### Per-Language Configuration

You can enable or disable Copilot for specific languages:

```json
{
  "github.copilot.enable": {
    "*": true,
    "markdown": true,
    "plaintext": false,
    "yaml": true
  }
}
```

### Agent Mode Settings

```json
{
  "chat.agent.enabled": true,
  "github.copilot.chat.agent.runTasks": true,
  "chat.mcp.enabled": true
}
```

---

## Step 6: Enable Copilot Chat Panel

1. Press `Ctrl+Shift+P` (or `Cmd+Shift+P`) to open the Command Palette
2. Type **"Copilot Chat: Open Chat"**
3. The Chat panel will appear on the left sidebar
4. You can also use the keyboard shortcut: `Ctrl+Alt+I` (Windows/Linux) or `Cmd+Option+I` (macOS)

### Chat Locations in VS Code

| Location | How to Open | Best For |
|----------|------------|---------|
| **Chat Panel** (sidebar) | `Ctrl+Alt+I` / `Cmd+Option+I` | Extended conversations, research |
| **Inline Chat** | `Ctrl+I` / `Cmd+I` | Quick edits in the current file |
| **Quick Chat** | `Ctrl+Shift+I` / `Cmd+Shift+I` | Fast questions, one-off queries |
| **Terminal Chat** | Type `@terminal` in chat | Terminal-related questions |

---

## Step 7: Select Your AI Model

1. Open Copilot Chat
2. Look for the **model selector dropdown** at the top of the chat panel
3. Click it to see available models:
   - GPT-4o (default)
   - Claude 3.5 Sonnet
   - Claude 3.7 Sonnet (Pro+/Enterprise)
   - Gemini 2.0 Flash
   - Gemini 2.5 Pro (Pro+/Enterprise)
   - o1 (Pro+/Enterprise — premium request)
   - o3-mini (Pro+/Enterprise — premium request)
4. Select your preferred model

> **Tip:** GPT-4o is fastest for completions. Claude excels at explanations and careful reasoning. Gemini is great for multimodal tasks.

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| No ghost text appearing | Check that `github.copilot.enable` is `true` in settings |
| "Not authorized" error | Sign out and sign back in via the Copilot status bar icon |
| Chat not available | Ensure the Copilot Chat extension is installed |
| Suggestions are slow | Check your internet connection; Copilot requires server access |
| Agent mode not showing | Update VS Code to the latest version (1.95+) |
| Wrong model selected | Click the model selector in chat panel to switch |

---

## Verification Checklist

- [ ] VS Code is installed and up to date
- [ ] GitHub Copilot extension is installed
- [ ] GitHub Copilot Chat extension is installed
- [ ] You are authenticated with your GitHub account
- [ ] Ghost text suggestions appear when you type code
- [ ] Copilot Chat opens and responds to questions
- [ ] You can see the model selector in the chat panel

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 02: Setup & Installation](README.md) |
| Next Lesson | [JetBrains IDE Setup](jetbrains-setup.md) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
