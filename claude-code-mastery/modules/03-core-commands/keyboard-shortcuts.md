# Keyboard Shortcuts

**Module 03, Lesson 3 — Claude Code Mastery**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Master these keyboard shortcuts to navigate Claude Code at maximum speed. All shortcuts work in the default (non-vim) mode unless noted otherwise.

---

## Essential Shortcuts

| Shortcut | Action | Context |
|----------|--------|---------|
| `Enter` | Send message | Input |
| `Shift+Enter` | New line (multiline input) | Input |
| `Ctrl+C` | Cancel current operation | During execution |
| `Ctrl+C × 2` | Exit Claude Code | Anytime |
| `Escape` | Cancel current input / dismiss menu | Input |

---

## Navigation & Input

| Shortcut | Action |
|----------|--------|
| `↑` / `↓` | Scroll through message history |
| `Ctrl+A` | Move cursor to beginning of line |
| `Ctrl+E` | Move cursor to end of line |
| `Ctrl+W` | Delete word backward |
| `Ctrl+U` | Delete entire line |
| `Ctrl+K` | Delete from cursor to end of line |
| `Ctrl+L` | Clear screen (keeps conversation) |
| `Tab` | Autocomplete file paths and commands |

---

## Mode Switching

| Shortcut | Action |
|----------|--------|
| `Shift+Tab` | Cycle permission modes: default → acceptEdits → plan → auto → bypass |
| `Alt+T` (or `Option+T`) | Toggle extended thinking on/off |
| `Ctrl+O` | Toggle verbose mode (see Claude's thinking) |

---

## Permission Prompts

When Claude asks for permission to run a tool:

| Key | Action |
|-----|--------|
| `y` | Allow this action once |
| `n` | Deny this action |
| `a` | Always allow this tool pattern |
| `Escape` | Cancel the current task |

---

## Context & Session

| Shortcut | Action |
|----------|--------|
| `Ctrl+G` | Open current content in external editor |
| `?` | Show help (in normal mode / vim normal mode) |

---

## Vim Mode Shortcuts

When vim mode is enabled (`/vim`), these additional shortcuts are available:

### Mode Switching

| Key | From | Action |
|-----|------|--------|
| `Esc` | INSERT | Enter NORMAL mode |
| `i` | NORMAL | Insert before cursor |
| `I` | NORMAL | Insert at beginning of line |
| `a` | NORMAL | Insert after cursor |
| `A` | NORMAL | Insert at end of line |
| `o` | NORMAL | Open line below |
| `O` | NORMAL | Open line above |

### Navigation (NORMAL mode)

| Key | Action |
|-----|--------|
| `h` / `j` / `k` / `l` | Left / Down / Up / Right |
| `w` | Jump to next word |
| `b` | Jump to previous word |
| `e` | Jump to end of word |
| `0` | Jump to beginning of line |
| `$` | Jump to end of line |
| `gg` | Jump to beginning of input |
| `G` | Jump to end of input |
| `f{char}` | Jump to next occurrence of char |
| `F{char}` | Jump to previous occurrence of char |
| `;` | Repeat last f/F forward |
| `,` | Repeat last f/F backward |

### Editing (NORMAL mode)

| Key | Action |
|-----|--------|
| `x` | Delete character under cursor |
| `dd` | Delete entire line |
| `D` | Delete from cursor to end of line |
| `dw` | Delete to next word |
| `db` | Delete to previous word |
| `cc` | Change entire line |
| `C` | Change from cursor to end of line |
| `cw` | Change word |
| `yy` / `Y` | Yank (copy) line |
| `yw` | Yank word |
| `p` | Paste after cursor |
| `P` | Paste before cursor |
| `>>` | Indent line |
| `<<` | Dedent line |
| `J` | Join current line with next |
| `.` | Repeat last editing command |
| `u` | Undo |

### Text Objects (use with d, c, y)

| Key | Selects |
|-----|---------|
| `iw` / `aw` | Inner / around word |
| `i"` / `a"` | Inner / around double quotes |
| `i'` / `a'` | Inner / around single quotes |
| `i(` / `a(` | Inner / around parentheses |
| `i{` / `a{` | Inner / around braces |
| `i[` / `a[` | Inner / around brackets |

### Examples

```
diw     → Delete inner word
ci"     → Change text inside double quotes
da(     → Delete around parentheses (including parens)
yaw     → Yank around word
```

---

## Custom Keybindings

You can customize keyboard shortcuts by editing `~/.claude/keybindings.json`:

```json
[
  {
    "key": "ctrl+s",
    "command": "chat:submit"
  },
  {
    "key": "ctrl+shift+c",
    "command": "chat:compact"
  }
]
```

### Available Commands for Keybindings

| Command | Description |
|---------|-------------|
| `chat:submit` | Send the current message |
| `chat:cancel` | Cancel current operation |
| `chat:compact` | Compact conversation |
| `chat:clear` | Clear conversation |
| `chat:help` | Show help |
| `chat:toggleVim` | Toggle vim mode |

### Chord Bindings

You can create two-key sequences:

```json
[
  {
    "key": "ctrl+k ctrl+c",
    "command": "chat:compact"
  }
]
```

For full keybinding customization details, use `/keybindings-help` inside Claude Code.

---

## Quick Reference Card

```
┌─────────────────────────────────────────────────┐
│          CLAUDE CODE KEYBOARD SHORTCUTS          │
├─────────────────────────────────────────────────┤
│                                                  │
│  BASICS                                          │
│  Enter .............. Send message               │
│  Shift+Enter ........ New line                   │
│  Ctrl+C ............. Cancel / Exit (×2)         │
│  Escape ............. Dismiss / Cancel            │
│  Tab ................ Autocomplete                │
│                                                  │
│  MODES                                           │
│  Shift+Tab .......... Cycle permission modes     │
│  Alt+T .............. Toggle thinking             │
│  Ctrl+O ............. Toggle verbose              │
│                                                  │
│  EDITING                                         │
│  Ctrl+A ............. Beginning of line           │
│  Ctrl+E ............. End of line                 │
│  Ctrl+W ............. Delete word back            │
│  Ctrl+U ............. Delete line                 │
│  Ctrl+K ............. Delete to end               │
│  Ctrl+L ............. Clear screen                │
│                                                  │
│  PERMISSIONS                                     │
│  y .................. Allow once                  │
│  n .................. Deny                        │
│  a .................. Always allow                │
│                                                  │
└─────────────────────────────────────────────────┘
```

---

**Next:** [CLI Flags & Options](cli-flags.md)

[← Back to Module Overview](README.md)

---

*Module 03, Lesson 3 — Claude Code Mastery — March 2026*
