# Claude Code: VS Code Extension

**Module 08, Lesson 2 — Claude Code Mastery**

**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Overview

The Claude Code extension for Visual Studio Code brings agentic AI directly into the editor you already use. It provides a dedicated panel for conversing with Claude, full access to your local workspace, and tight integration with VS Code features like the terminal, file explorer, and editor tabs. This lesson covers installation, configuration, and practical tips for getting the most out of Claude Code inside VS Code.

---

## Installation from the VS Code Marketplace

1. Open VS Code.
2. Go to the Extensions view (`Ctrl+Shift+X` / `Cmd+Shift+X`).
3. Search for **"Claude Code"** by Anthropic.
4. Click **Install**.
5. Reload VS Code if prompted.

Alternatively, install from the command line:

```bash
code --install-extension anthropic.claude-code
```

After installation, authenticate by signing in with your Anthropic account when prompted.

---

## Opening the Claude Code Panel

There are several ways to open the Claude Code panel:

| Method | Action |
|--------|--------|
| Activity Bar | Click the Claude Code icon in the left sidebar |
| Command Palette | `Ctrl+Shift+P` then type "Claude Code: Open Panel" |
| Keyboard shortcut | `Ctrl+Shift+L` / `Cmd+Shift+L` (default binding) |
| Terminal | Run `claude` in the VS Code integrated terminal |

The panel opens as a side view where you can type prompts and see Claude's responses, code changes, and tool activity in real time.

---

## How It Integrates with the Editor

The extension has deep access to your VS Code workspace:

| Integration Point | Description |
|--------------------|-------------|
| Open files | Claude can see and reference files currently open in editor tabs |
| Workspace files | Full read/write access to all files in the workspace |
| Active selection | Highlight code and ask Claude about the selection |
| Diagnostics | Claude can see linting errors, warnings, and problems from VS Code |
| Source control | Integrates with Git through the VS Code SCM panel |
| File explorer | Can navigate and create files through the workspace tree |

**Example workflow — fixing a highlighted error:**

1. Highlight a function with a red squiggly underline.
2. Open the Claude Code panel.
3. Type: "Fix the type error in my selection."
4. Claude reads the selection, diagnostics, and surrounding context, then applies a fix.

---

## Using Claude Code Alongside VS Code Features

Claude Code works best when combined with native VS Code capabilities:

- **Split view** — Keep Claude Code in a side panel while editing in the main area.
- **Multi-root workspaces** — Claude can access all folders in a multi-root workspace.
- **Tasks** — Claude can trigger VS Code tasks defined in `tasks.json`.
- **Debugging** — Ask Claude to help set up `launch.json` configurations or interpret debug output.
- **Extensions** — Claude works alongside other extensions (ESLint, Prettier, GitLens, etc.).

---

## Terminal Integration

The VS Code extension can interact with the integrated terminal:

```bash
# Claude can run commands in the VS Code terminal
npm run test
python -m pytest
git status
```

| Terminal Feature | Behavior |
|------------------|----------|
| Command execution | Claude runs commands in the integrated terminal |
| Output capture | Terminal output is read back into the conversation |
| Multiple terminals | Claude can create and use multiple terminal instances |
| Shell selection | Inherits your configured default shell (bash, zsh, PowerShell) |

---

## Settings and Configuration

Configure the extension through VS Code settings (`Ctrl+,` / `Cmd+,`):

```json
// .vscode/settings.json
{
  "claudeCode.model": "claude-sonnet-4-20250514",
  "claudeCode.terminalAutoRun": true,
  "claudeCode.showInlineCompletions": false,
  "claudeCode.maxTokensPerRequest": 8192,
  "claudeCode.apiKey": "",
  "claudeCode.hooks.enabled": true
}
```

| Setting | Description | Default |
|---------|-------------|---------|
| `model` | Which Claude model to use | `claude-sonnet-4-20250514` |
| `terminalAutoRun` | Auto-execute terminal commands | `true` |
| `showInlineCompletions` | Show inline code suggestions | `false` |
| `maxTokensPerRequest` | Max tokens per API call | `8192` |
| `hooks.enabled` | Enable hook execution | `true` |

Your project-level `.claude/settings.json` and `CLAUDE.md` files are fully respected by the extension.

---

## Tips for VS Code Users

1. **Use `@workspace`** — Reference your entire workspace context in prompts.
2. **Pin the panel** — Keep the Claude Code panel pinned so it persists across sessions.
3. **Keyboard-first workflow** — Use `Ctrl+Shift+L` to open the panel, type your prompt, and press Enter without touching the mouse.
4. **Leverage selections** — Select code before prompting to give Claude focused context.
5. **Check the Problems panel** — After Claude makes changes, review the Problems panel for new diagnostics.
6. **Use `.claude/` config** — Your project CLAUDE.md and hook configurations work identically in the extension.
7. **Combine with Source Control** — Ask Claude to stage and commit after making changes.

---

## Navigation

| Direction | Link |
|-----------|------|
| Previous | [Claude Code on the Web](claude-code-web.md) |
| Next | [JetBrains Extension](jetbrains-extension.md) |
| Home | [Course Home](../../) |
