# JetBrains IDE Setup

**Module 02, Lesson 2 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

GitHub Copilot is fully supported in all JetBrains IDEs — IntelliJ IDEA, PyCharm, WebStorm, GoLand, PhpStorm, Rider, CLion, RubyMine, and more. This lesson covers installation, authentication, and configuration.

---

## Supported JetBrains IDEs

| IDE | Primary Language | Copilot Support |
|-----|-----------------|----------------|
| IntelliJ IDEA | Java, Kotlin | Full |
| PyCharm | Python | Full |
| WebStorm | JavaScript, TypeScript | Full |
| GoLand | Go | Full |
| PhpStorm | PHP | Full |
| Rider | C#, .NET | Full |
| CLion | C, C++ | Full |
| RubyMine | Ruby | Full |
| DataGrip | SQL | Full |
| Android Studio | Java, Kotlin | Full |

> **Minimum Version:** JetBrains IDE version 2023.3 or later recommended.

---

## Step 1: Install the GitHub Copilot Plugin

1. Open your JetBrains IDE
2. Go to **Settings/Preferences** (`Ctrl+Alt+S` on Windows/Linux, `Cmd+,` on macOS)
3. Navigate to **Plugins** → **Marketplace**
4. Search for **"GitHub Copilot"**
5. Click **Install**
6. Restart the IDE when prompted

---

## Step 2: Authenticate with GitHub

1. After restarting, go to **Settings** → **GitHub Copilot**
2. Click **"Sign in to GitHub"**
3. A device code will be displayed — copy it
4. A browser window opens to [github.com/login/device](https://github.com/login/device)
5. Paste the device code
6. Authorize the JetBrains plugin
7. Return to your IDE — authentication should be confirmed

---

## Step 3: Configure Settings

Navigate to **Settings** → **GitHub Copilot** to configure:

### Completion Settings

- **Enable completions:** Toggle inline code suggestions on/off
- **Automatic suggestions:** Show suggestions as you type (vs. manual trigger)
- **Language-specific settings:** Enable/disable for specific file types

### Chat Settings

- **Enable Copilot Chat:** Available in the tool window
- **Model selection:** Choose between available AI models

---

## Step 4: Using Copilot in JetBrains

### Inline Completions

- Suggestions appear as **gray ghost text** as you type
- Press **Tab** to accept the full suggestion
- Press **Alt+]** to see the next suggestion
- Press **Alt+[** to see the previous suggestion
- Press **Escape** to dismiss

### Copilot Chat

1. Open the **Copilot Chat** tool window (usually on the right sidebar)
2. Type your question or request
3. Use `/explain`, `/fix`, `/tests` slash commands
4. Reference files with `#file:` syntax

### Keyboard Shortcuts (JetBrains)

| Action | Windows/Linux | macOS |
|--------|--------------|-------|
| Accept suggestion | `Tab` | `Tab` |
| Next suggestion | `Alt+]` | `Option+]` |
| Previous suggestion | `Alt+[` | `Option+[` |
| Dismiss suggestion | `Escape` | `Escape` |
| Trigger suggestion manually | `Alt+\` | `Option+\` |
| Open Copilot Chat | Via tool window | Via tool window |
| Inline chat | `Ctrl+Shift+I` | `Cmd+Shift+I` |

---

## JetBrains vs. VS Code Feature Comparison

| Feature | VS Code | JetBrains |
|---------|---------|-----------|
| Inline completions | Yes | Yes |
| Copilot Chat | Yes | Yes |
| Copilot Edits | Yes | Yes (2025+) |
| Agent Mode | Yes (full) | Limited (2026) |
| MCP Support | Yes | Coming Soon |
| Next Edit Suggestions | Yes | Coming Soon |
| Inline Chat | Yes | Yes |
| Model Selection | Yes | Yes |
| Vision (images) | Yes | Limited |

> **Note:** VS Code remains the most feature-complete environment for Copilot. JetBrains support is rapidly expanding but may lag slightly behind VS Code for the newest features like agent mode.

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 02: Setup & Installation](README.md) |
| Previous Lesson | [VS Code Setup](vs-code-setup.md) |
| Next Lesson | [Neovim & Xcode Setup](neovim-xcode-setup.md) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
