# Lesson 1: Desktop App Setup

**Module 02, Lesson 1 | Claude Cowork Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Before you can work with Claude Cowork, you need to understand the tool you will be using every day: the Claude Desktop application. This lesson walks you through the interface, shows you where every important setting lives, and helps you configure the app for the best possible Cowork experience.

---

## 1. Interface Walkthrough

When you open Claude Desktop, you will see several key areas:

### Main Chat Panel

- This is the large central area where your conversation with Claude takes place.
- Messages you send appear on the right; Claude's responses appear on the left.
- File previews, code blocks, and action confirmations all display inline here.

### Sidebar

- **Conversation History** — A list of your past conversations, organised by date. Click any entry to reopen it.
- **Starred Conversations** — Pin important conversations for quick access.
- **New Conversation** — The button at the top starts a fresh session.

### Top Menu Bar

- **File** — Create new conversations, open saved sessions, and export conversation logs.
- **Edit** — Standard text editing options (copy, paste, undo) plus conversation-specific actions like clearing the current chat.
- **Settings** — Access all application and Cowork preferences (covered in detail below).
- **Help** — Links to documentation, release notes, and support channels.
- **Model Selector** — Choose which Claude model to use (select a model that supports Cowork/agent features).
- **Account Menu** — Access your profile, subscription details, and sign-out option.

### Status Indicators

- Look for the Cowork status badge near the top of the chat panel. When Cowork is active, you will see a distinct indicator confirming that agent capabilities are enabled for the current session.
- The **Status Bar** at the bottom of the window shows connection status, the current model in use, and any active background tasks.

---

## 2. Configuring Cowork Preferences

Follow these steps to set up Cowork for the first time:

### Step 1: Open Settings

- Click the **gear icon** in the bottom-left corner of the sidebar, or use the keyboard shortcut (`Ctrl + ,` on Windows / `Cmd + ,` on macOS).

### Step 2: Navigate to the Cowork Section

- In the Settings panel, select the **"Cowork"** or **"Agent"** tab.
- This is where all agent-specific options are managed.

### Step 3: Set Your Default Behaviour

| Setting | Recommended Value | Notes |
|---------|-------------------|-------|
| Default Mode | **Cowork** | Ensures Claude starts in agent mode by default. |
| Working Directory | Your main projects folder | Example: `C:\Users\You\Projects` or `~/Projects` |
| Action Confirmation | **Always ask** | Claude will ask before creating, editing, or deleting files. Recommended for beginners. |
| File Operation Mode | **Read and Write** | Allows Claude to view, create, and edit files in permitted folders. |
| Terminal Access | **Off** | Keep this off if you are non-technical until you are more comfortable. |

### Step 4: Save Your Preferences

- Click **Save** or **Apply**. Your preferences take effect immediately for new conversations.

---

## 3. Enabling Agent Features

Cowork capabilities may need to be explicitly enabled:

1. In the Cowork settings section, locate the **"Enable Cowork Mode"** toggle.
2. Switch it **on**.
3. You may be prompted to accept additional terms of use — read them and confirm.
4. Once enabled, new conversations will display the Cowork status badge, confirming that Claude can take actions on your behalf.
5. Review the individual feature toggles:
   - **File Operations** — Allows Claude to read, create, and edit files in permitted folders.
   - **Command Execution** — Allows Claude to run terminal commands on your behalf (with confirmation).
   - **Web Access** — Allows Claude to fetch information from URLs when needed.
6. Leave any features you are unsure about set to **Off** for now. You can always enable them later as you gain confidence.

> **Note:** If you do not see the Cowork toggle, make sure your Claude Desktop app is updated to the latest version and that your subscription plan includes agent features.

---

## 4. Notification Settings

Stay informed without being overwhelmed:

| Setting | Recommended Value | Why |
|---------|-------------------|-----|
| Task Completion Alerts | **On** | Know when Claude finishes a task. |
| Confirmation Required | **On** | Get alerted when Claude needs your approval before proceeding. |
| Error Alerts | **On** | Be notified immediately if something goes wrong. |
| Background Task Updates | **On** | Useful if you run longer tasks and switch to another app. |
| Sound Notifications | **Your preference** | Turn on if you step away from the screen often; turn off if they are distracting. |

To adjust these:

1. Go to **Settings > Notifications**.
2. Toggle each notification type on or off.
3. Save your changes.

---

## 5. Tips for Optimal Setup

- **Use a dedicated work folder.** Create a folder like `Claude-Projects` on your desktop or in your Documents directory. Point Claude to this folder so it has a clean workspace.
- **Start with conservative permissions.** You can always grant more access later. Begin with confirmation prompts enabled and terminal access off.
- **Keep the app updated.** Cowork features are actively developed. Check for updates under **Help > Check for Updates** at least once a week.
- **Customise your sidebar.** Pin your most-used projects to the sidebar for quick access. Right-click any conversation and select **Pin to Sidebar**.
- **Learn the keyboard shortcuts.** A few worth memorising early:
  - `Ctrl/Cmd + N` — New conversation
  - `Ctrl/Cmd + ,` — Open Settings
  - `Ctrl/Cmd + Shift + P` — Command palette
- **Bookmark the settings page.** You will revisit preferences as you grow more comfortable and want to adjust your workflow.

---

## Summary

You should now have:

- A clear understanding of the Claude Desktop interface layout
- Cowork preferences configured to your comfort level
- Agent features enabled and confirmed
- Notification settings tailored to your workflow

In the next lesson, you will learn how to grant Claude access to your project folders safely and securely.

---

## Navigation

| | |
|---|---|
| [Back to Module 02 Overview](README.md) | Return to the module page |
| [Next Lesson: Folder Access](folder-access.md) | Lesson 2 |

---

*Claude Cowork Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
