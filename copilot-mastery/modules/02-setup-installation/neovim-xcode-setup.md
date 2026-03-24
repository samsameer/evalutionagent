# Neovim & Xcode Setup

**Module 02, Lesson 3 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

GitHub Copilot supports Neovim for terminal-centric developers and Xcode for Apple platform developers. This lesson covers setup for both editors.

---

## Part 1: Neovim Setup

### Prerequisites

- Neovim **0.6 or later** (0.9+ recommended)
- Node.js **18 or later** installed
- A GitHub account with Copilot access

### Step 1: Install the Copilot Plugin

Using your preferred plugin manager:

**With vim-plug:**
```vim
Plug 'github/copilot.vim'
```

**With lazy.nvim:**
```lua
{
  "github/copilot.vim",
}
```

**With packer.nvim:**
```lua
use 'github/copilot.vim'
```

Then reload your configuration and install plugins.

### Step 2: Authenticate

Run the following command inside Neovim:

```
:Copilot setup
```

This will:
1. Display a one-time device code
2. Open your browser to [github.com/login/device](https://github.com/login/device)
3. Enter the code to authorize
4. Confirm authentication in Neovim

### Step 3: Verify

```
:Copilot status
```

You should see: `GitHub Copilot: Ready`

### Step 4: Usage

| Action | Keybinding |
|--------|-----------|
| Accept suggestion | `Tab` |
| Dismiss suggestion | `Ctrl+]` |
| Next suggestion | `Alt+]` |
| Previous suggestion | `Alt+[` |
| Trigger suggestion | `:Copilot suggest` |
| Open panel | `:Copilot panel` |

### Copilot Chat for Neovim

For Copilot Chat in Neovim, use the community plugin:

```lua
-- With lazy.nvim
{
  "CopilotC-Nvim/CopilotChat.nvim",
  dependencies = {
    { "github/copilot.vim" },
    { "nvim-lua/plenary.nvim" },
  },
  opts = {},
}
```

---

## Part 2: Xcode Setup

### Prerequisites

- Xcode **16.0 or later**
- macOS **14 (Sonoma)** or later
- A GitHub account with Copilot access

### Step 1: Enable Copilot in Xcode

GitHub Copilot for Xcode runs as a **separate companion app**:

1. Download **GitHub Copilot for Xcode** from [github.com/github/CopilotForXcode](https://github.com/github/CopilotForXcode)
2. Install the application
3. Open the app and sign in with your GitHub account
4. Grant the necessary permissions (Accessibility access)
5. The app runs in the background and provides suggestions in Xcode

### Step 2: Configure

1. Open the **GitHub Copilot for Xcode** app
2. Navigate to **Settings**
3. Configure:
   - Enable/disable suggestions
   - Suggestion trigger delay
   - Language preferences (Swift, Objective-C, C, C++)

### Step 3: Usage in Xcode

- Suggestions appear as **ghost text** in the editor
- Press **Tab** to accept
- Press **Escape** to dismiss
- The companion app icon in the menu bar shows status

### Xcode Feature Support

| Feature | Supported |
|---------|-----------|
| Inline completions | Yes |
| Ghost text | Yes |
| Multi-line suggestions | Yes |
| Copilot Chat | Limited (via companion app) |
| Agent Mode | No |
| Copilot Edits | No |

> **Note:** Xcode support is more limited compared to VS Code. For the full Copilot experience with agent mode, consider using VS Code alongside Xcode for non-UI development tasks.

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 02: Setup & Installation](README.md) |
| Previous Lesson | [JetBrains IDE Setup](jetbrains-setup.md) |
| Next Lesson | [Copilot CLI Installation](cli-installation.md) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
