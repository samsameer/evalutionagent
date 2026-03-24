# Completions Panel & Navigation

**Module 03, Lesson 3 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Sometimes the first suggestion is not the best one. The Copilot Completions Panel lets you view **multiple alternative suggestions** side by side, compare them, and choose the best one. This lesson covers how to navigate suggestions and use the panel effectively.

---

## Navigating Between Suggestions

When Copilot shows a ghost text suggestion, there may be multiple alternatives available. You can cycle through them without opening the full panel:

| Action | Windows/Linux | macOS |
|--------|--------------|-------|
| Next suggestion | `Alt+]` | `Option+]` |
| Previous suggestion | `Alt+[` | `Option+[` |
| Accept current | `Tab` | `Tab` |
| Dismiss all | `Escape` | `Escape` |

---

## Opening the Completions Panel

To see all suggestions at once in a dedicated panel:

1. Press `Ctrl+Shift+Alt+]` (Windows/Linux) — or use the Command Palette
2. Or: Open Command Palette (`Ctrl+Shift+P`) → "GitHub Copilot: Open Completions Panel"

The panel shows **up to 10 alternative suggestions** for the current cursor position.

### Panel Features

| Feature | Description |
|---------|-------------|
| Multiple suggestions | See 3-10 alternatives at once |
| Syntax highlighting | Each suggestion is properly highlighted |
| Accept button | Click to accept a specific suggestion |
| Diff view | See what each suggestion would add/change |

---

## When to Use the Panel vs. Inline Navigation

### Use Inline Navigation (`Alt+]`/`Alt+[`) When:
- You want to quickly check 2-3 alternatives
- You have a general idea of what you want
- Speed is more important than comparison

### Use the Completions Panel When:
- You want to see all options at once
- The task is complex (algorithm, architecture decision)
- You want to compare different approaches
- You are learning and want to see what patterns Copilot knows

---

## Triggering Suggestions Manually

If Copilot does not automatically show a suggestion, you can manually trigger one:

| Action | Windows/Linux | macOS |
|--------|--------------|-------|
| Trigger inline suggestion | `Alt+\` | `Option+\` |

This is useful when:
- You have stopped typing and Copilot's auto-trigger window has passed
- You want a fresh suggestion after editing context
- You want suggestions at an unusual cursor position

---

## Fine-Tuning Completion Behavior

### Adjusting Trigger Timing

In VS Code settings:

```json
{
  // Delay before showing suggestions (milliseconds)
  "editor.quickSuggestionsDelay": 10,

  // Enable automatic inline suggestions
  "github.copilot.editor.enableAutoCompletions": true,

  // Show suggestions in comments
  "github.copilot.editor.enableCodeActions": true
}
```

### Disabling for Specific Contexts

```json
{
  "github.copilot.enable": {
    "*": true,
    "markdown": false,    // Disable in markdown files
    "plaintext": false,    // Disable in plain text
    "scminput": false      // Disable in git commit messages
  }
}
```

---

## Completion Quality Indicators

While Copilot does not show a confidence score, you can gauge suggestion quality by:

1. **Speed of appearance** — Faster suggestions often mean higher confidence
2. **Length of suggestion** — Longer, more detailed suggestions indicate strong context understanding
3. **Consistency across alternatives** — If multiple suggestions are similar, the pattern is well understood
4. **Match with your patterns** — Copilot learns your coding style from open files

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 03: VS Code Core](README.md) |
| Previous Lesson | [Next Edit Suggestions (NES)](next-edit-suggestions.md) |
| Next Module | [Module 04: Copilot Chat Deep Dive](../04-copilot-chat/) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
