# Claude Code: JetBrains Extension

**Module 08, Lesson 3 — Claude Code Mastery**

**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Overview

The Claude Code plugin for JetBrains IDEs brings the same agentic coding experience into IntelliJ IDEA, PyCharm, WebStorm, and other JetBrains products. This lesson covers installation, supported IDEs, configuration, and how the JetBrains integration differs from the VS Code extension.

---

## Installation from the JetBrains Marketplace

1. Open your JetBrains IDE.
2. Go to **Settings/Preferences** (`Ctrl+Alt+S` / `Cmd+,`).
3. Navigate to **Plugins > Marketplace**.
4. Search for **"Claude Code"** by Anthropic.
5. Click **Install** and restart the IDE when prompted.

Alternatively, install from the JetBrains Marketplace website and it will open in your IDE automatically.

The plugin also detects the Claude Code CLI if already installed via `npm install -g @anthropic-ai/claude-code`.

---

## Supported IDEs

The Claude Code plugin works across the JetBrains IDE family:

| IDE | Language Focus | Supported |
|-----|---------------|-----------|
| IntelliJ IDEA | Java, Kotlin, Scala | Yes |
| PyCharm | Python | Yes |
| WebStorm | JavaScript, TypeScript | Yes |
| GoLand | Go | Yes |
| Rider | C#, .NET | Yes |
| CLion | C, C++ | Yes |
| PhpStorm | PHP | Yes |
| RubyMine | Ruby | Yes |
| DataGrip | SQL, Databases | Yes |

**Minimum version requirement:** 2024.1 or later for all IDEs.

---

## How It Integrates with JetBrains

The plugin provides a tool window panel and integrates with the JetBrains platform:

| Integration Point | Description |
|--------------------|-------------|
| Tool window | Dedicated Claude Code panel in the side bar |
| Project files | Full read/write access to all project files |
| Editor selections | Send highlighted code to Claude for analysis |
| Run configurations | Claude can read and create run/debug configurations |
| Terminal | Access to the built-in terminal for command execution |
| VCS integration | Works with Git, Mercurial, and other VCS providers |
| Inspections | Claude can see IDE inspections and warnings |

**Opening the panel:**

| Method | Action |
|--------|--------|
| Tool window bar | Click "Claude Code" in the right-side tool window bar |
| Menu | **View > Tool Windows > Claude Code** |
| Shortcut | `Alt+C` (default binding) |
| Find Action | `Ctrl+Shift+A` then type "Claude Code" |

---

## Configuration

Plugin settings are available under **Settings > Tools > Claude Code**:

```json
// Equivalent settings in .claude/settings.json (project-level)
{
  "model": "claude-sonnet-4-20250514",
  "permissions": {
    "allow": ["Read", "Write", "Bash"],
    "deny": ["Bash(rm -rf *)"]
  },
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Write",
        "hooks": [
          {
            "type": "command",
            "command": "echo 'File write detected'"
          }
        ]
      }
    ]
  }
}
```

| Setting | Location | Description |
|---------|----------|-------------|
| API key | IDE Settings > Claude Code | Your Anthropic API key or SSO login |
| Model selection | IDE Settings > Claude Code | Choose the Claude model |
| Auto-run commands | IDE Settings > Claude Code | Allow automatic terminal execution |
| Project config | `.claude/settings.json` | Project-specific settings (shared with CLI) |
| Memory file | `CLAUDE.md` | Project context (shared with CLI) |

The plugin fully respects your existing `.claude/` directory, `CLAUDE.md` files, and hook configurations — the same project setup works across CLI, VS Code, and JetBrains.

---

## Differences from the VS Code Extension

| Aspect | VS Code Extension | JetBrains Plugin |
|--------|-------------------|------------------|
| Install source | VS Code Marketplace | JetBrains Marketplace |
| Panel location | Side bar (Activity Bar) | Tool window (right side) |
| Keyboard shortcut | `Ctrl+Shift+L` | `Alt+C` |
| Inline completions | Supported | Supported |
| Diagnostics access | VS Code Problems panel | JetBrains Inspections |
| Multi-root projects | Native support | Module-based support |
| Terminal | VS Code integrated terminal | JetBrains built-in terminal |
| Config format | `.vscode/settings.json` + `.claude/` | IDE settings + `.claude/` |
| Refactoring tools | Limited IDE integration | Deep refactoring integration |
| Database tools | Requires extensions | Native in DataGrip/IntelliJ Ultimate |

Both extensions share the same Claude Code engine and respect the same project configuration. JetBrains offers deeper refactoring and inspection integration, while VS Code offers a broader extension ecosystem.

---

## Tips for JetBrains Users

1. **Use IDE inspections** — Ask Claude to fix all warnings reported by the JetBrains inspector.
2. **Leverage run configurations** — Have Claude create and modify run/debug configurations.
3. **Database integration** — In DataGrip or IntelliJ Ultimate, Claude can work with database consoles.
4. **Reformat after changes** — Use the IDE's reformat action (`Ctrl+Alt+L`) after Claude edits code.
5. **Share `.claude/` config** — Your project configuration works identically across CLI and both IDE extensions.

---

## Navigation

| Direction | Link |
|-----------|------|
| Previous | [VS Code Extension](vs-code-extension.md) |
| Next | [Desktop App](desktop-app.md) |
| Home | [Course Home](../../) |
