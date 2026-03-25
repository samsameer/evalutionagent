# Claude Code: Desktop App (Mac/Windows)

**Module 08, Lesson 4 — Claude Code Mastery**

**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Overview

The Claude Code Desktop App is a standalone native application for Mac and Windows that combines the local file access of the CLI with a polished graphical interface. This lesson covers installation, how the desktop app differs from the CLI, system integration features, and best use cases.

---

## Availability

| Platform | Supported | Minimum Version |
|----------|-----------|-----------------|
| macOS | Yes | macOS 13 (Ventura) or later |
| Windows | Yes | Windows 10 (64-bit) or later |
| Linux | Not available | Use the CLI instead |

---

## Installation

### macOS

1. Download from [claude.ai/download](https://claude.ai/download) or the Mac App Store.
2. Open the `.dmg` and drag **Claude Code** into Applications.
3. Launch the app and sign in with your Anthropic account.

```bash
# Or install via Homebrew
brew install --cask claude-code
```

### Windows

1. Download from [claude.ai/download](https://claude.ai/download) or the Microsoft Store.
2. Run the installer and follow the prompts.
3. Sign in with your Anthropic account.

```powershell
# Or install via winget
winget install Anthropic.ClaudeCode
```

---

## How It Differs from the CLI

| Feature | CLI | Desktop App |
|---------|-----|-------------|
| Interface | Terminal-based | Native graphical UI |
| Launch method | `claude` command in shell | App icon or system launcher |
| File access | Current working directory | Choose project folder via UI |
| Output rendering | Plain text / ANSI | Rich Markdown, syntax highlighting |
| Image support | Limited | Full image preview and drag-and-drop |
| Notifications | None | Native OS notifications on completion |
| Multi-session | Multiple terminal tabs | Built-in tabbed sessions |
| Configuration | `.claude/settings.json` | GUI settings + `.claude/settings.json` |
| Hooks and MCP | Full support | Full support |

All project-level configurations, hooks, MCP servers, and CLAUDE.md files work identically.

---

## Project Setup in the Desktop App

When you launch the desktop app, you can open a project in several ways:

| Method | Action |
|--------|--------|
| Open Folder | **File > Open Folder** to select a project directory |
| Drag and drop | Drag a folder onto the app window |
| Recent projects | Select from the recently opened list |
| Command line | `claude-desktop /path/to/project` |

Once a project is open, Claude has full read/write access to all files in that directory, just like the CLI.

---

## Integration with System Features

The desktop app takes advantage of native operating system capabilities:

| Feature | macOS | Windows |
|---------|-------|---------|
| Notifications | macOS Notification Center | Windows Action Center |
| File associations | Open files from Finder | Open files from Explorer |
| System search | Appears in Spotlight | Appears in Start search |
| Clipboard / Dark mode | Full support, follows system theme | Full support, follows system theme |
| Auto-update | Background updates | Background updates |

The app also supports a system tray (Windows) or menu bar (macOS) mode for quick access to new sessions and notifications without opening the full window.

---

## Settings and Configuration

The desktop app provides a GUI settings panel and respects your file-based configuration:

```json
{
  "model": "claude-sonnet-4-20250514",
  "permissions": {
    "allow": ["Read", "Write", "Bash"],
    "deny": []
  }
}
```

| Setting | Description | Default |
|---------|-------------|---------|
| Theme | UI theme: light, dark, or system | System |
| Notifications | Enable OS notifications | Enabled |
| Start in tray | Launch minimized to tray/menu bar | Disabled |
| Default project path | Default folder for new sessions | Home directory |

---

## Best Use Cases

| Use Case | Why the Desktop App Works Well |
|----------|--------------------------------|
| Dedicated coding sessions | Full-screen native window without terminal clutter |
| Visual projects | Rich rendering of images, Markdown, and diagrams |
| Multi-project work | Tabbed sessions let you switch between projects |
| Non-terminal users | Approachable GUI for developers less comfortable with CLI |
| Long-running tasks | System notifications alert you when tasks complete |

---

## Tips for Desktop App Users

1. **Use tabs** — Open multiple project sessions in separate tabs to work across repos.
2. **Enable notifications** — Let the OS notify you when Claude finishes long tasks.
3. **Drag files in** — Drop files or images directly into the chat for quick context.
4. **Keep `.claude/` consistent** — Your config is shared across CLI, VS Code, JetBrains, and the desktop app.

---

## Navigation

| Direction | Link |
|-----------|------|
| Previous | [JetBrains Extension](jetbrains-extension.md) |
| Next | [Module 09: Team & Enterprise](../09-team-enterprise/) |
| Home | [Course Home](../../) |
