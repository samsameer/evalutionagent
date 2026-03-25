# Keyboard Shortcuts Reference

**Module 11, Lesson 2 — Claude Code Mastery**

**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Overview

This is a print-ready keyboard shortcut reference card for Claude Code. All shortcuts are organized by category. Where macOS and Linux differ, both are listed.

---

## Print-Ready Reference Card

```
╔══════════════════════════════════════════════════════════════════════╗
║                  CLAUDE CODE — KEYBOARD SHORTCUTS                  ║
╠══════════════════════════════════════════════════════════════════════╣
║                                                                    ║
║  INPUT                                                             ║
║  ─────────────────────────────────────────────────────────────────  ║
║  Enter ................... Send message / submit prompt             ║
║  Shift+Enter ............. Insert a new line (multi-line input)     ║
║  Escape .................. Cancel current input / close menu        ║
║  Up Arrow ................ Scroll through input history (prev)      ║
║  Down Arrow .............. Scroll through input history (next)      ║
║  Tab ..................... Accept autocomplete suggestion            ║
║  Ctrl+C .................. Interrupt running operation / cancel      ║
║  Ctrl+D .................. Exit Claude Code (end session)            ║
║                                                                    ║
║  EDITING                                                           ║
║  ─────────────────────────────────────────────────────────────────  ║
║  Ctrl+A .................. Move cursor to beginning of line         ║
║  Ctrl+E .................. Move cursor to end of line               ║
║  Ctrl+U .................. Delete from cursor to start of line      ║
║  Ctrl+K .................. Delete from cursor to end of line        ║
║  Ctrl+W .................. Delete word before cursor                ║
║  Alt+Backspace ........... Delete word before cursor (alt)          ║
║  Ctrl+L .................. Clear the screen                         ║
║                                                                    ║
║  NAVIGATION & OUTPUT                                               ║
║  ─────────────────────────────────────────────────────────────────  ║
║  Scroll Up ............... Scroll up through output history         ║
║  Scroll Down ............. Scroll down through output history       ║
║  Ctrl+C .................. Stop Claude's current response           ║
║                                                                    ║
║  MODES                                                             ║
║  ─────────────────────────────────────────────────────────────────  ║
║  /vim .................... Toggle Vim keybinding mode               ║
║  /compact ................ Compact conversation to save context     ║
║  /clear .................. Clear conversation history entirely      ║
║  /model <name> ........... Switch to a different model              ║
║                                                                    ║
║  PERMISSIONS                                                       ║
║  ─────────────────────────────────────────────────────────────────  ║
║  y / Enter ............... Approve a tool action                    ║
║  n ....................... Deny a tool action                       ║
║  a ....................... Always allow this specific action         ║
║  d ....................... Deny and provide alternate instructions   ║
║  ? ....................... Show permission help                      ║
║                                                                    ║
║  VIM MODE (toggle with /vim)                                       ║
║  ─────────────────────────────────────────────────────────────────  ║
║  i ....................... Enter insert mode                        ║
║  Escape .................. Return to normal mode                    ║
║  h / j / k / l ........... Move left / down / up / right           ║
║  w / b ................... Move forward / backward by word          ║
║  0 / $ ................... Move to start / end of line              ║
║  x ....................... Delete character under cursor            ║
║  dd ...................... Delete entire line                       ║
║  yy ...................... Yank (copy) entire line                  ║
║  p ....................... Paste after cursor                       ║
║  u ....................... Undo last change                         ║
║  A ....................... Append at end of line (enter insert)     ║
║  I ....................... Insert at beginning of line              ║
║  o ....................... Open new line below (enter insert)       ║
║  O ....................... Open new line above (enter insert)       ║
║                                                                    ║
╠══════════════════════════════════════════════════════════════════════╣
║                                                                    ║
║  PLATFORM DIFFERENCES                                              ║
║  ─────────────────────────────────────────────────────────────────  ║
║                                                                    ║
║  Shortcut        macOS              Linux                          ║
║  ─────────────   ──────────────     ──────────────                 ║
║  Copy            Cmd+C              Ctrl+Shift+C                   ║
║  Paste           Cmd+V              Ctrl+Shift+V                   ║
║  Clear screen    Cmd+K or Ctrl+L    Ctrl+L                         ║
║  Open settings   Cmd+,              (use /config)                  ║
║  Word back       Alt+B / Opt+Left   Alt+B                          ║
║  Word forward    Alt+F / Opt+Right  Alt+F                          ║
║  Delete word     Opt+Backspace      Ctrl+W                         ║
║                                                                    ║
╠══════════════════════════════════════════════════════════════════════╣
║                                                                    ║
║  QUICK SLASH COMMANDS                                              ║
║  ─────────────────────────────────────────────────────────────────  ║
║  /help ......... Show all commands   /status ...... Session info    ║
║  /doctor ....... Run diagnostics     /cost ........ Token usage     ║
║  /init ......... Create CLAUDE.md    /memory ...... Edit CLAUDE.md  ║
║  /login ........ Authenticate        /logout ...... Sign out        ║
║  /review ....... Code review         /pr-review ... PR review       ║
║  /config ....... Open settings       /bug ......... Report bug      ║
║  /permissions .. View/edit perms     /terminal-setup  Terminal cfg  ║
║                                                                    ║
╚══════════════════════════════════════════════════════════════════════╝
```

---

## Printing Tips

1. **Monospace font required.** Use Courier New, Consolas, or any monospaced font so the ASCII art box lines up.
2. **Landscape orientation** works best if you want it on a single page.
3. **Font size 8-9pt** fits everything on one US Letter or A4 page in landscape.
4. **Terminal print:** run `cat keyboard-shortcuts-reference.md | lp` on Linux or use File > Print in your terminal on macOS.

---

## Notes on Shortcuts

- **Ctrl+C behavior** depends on context: if Claude is generating, it stops the response; if you are typing, it cancels the current input; if nothing is happening, it does nothing.
- **Vim mode** persists across the session but resets when you restart Claude Code. To make it permanent, add a note in your `~/.claude/CLAUDE.md` or start with `/vim` in each session.
- **Permission prompts** appear inline. You cannot use Ctrl shortcuts while a permission prompt is active; only the listed keys (y/n/a/d/?) work.
- **Scroll behavior** depends on your terminal emulator. Most modern terminals support mouse scroll and Shift+PageUp/PageDown.

---

## Navigation

| Direction | Link |
|-----------|------|
| Previous Lesson | [Complete Command Reference](command-reference.md) |
| Next Lesson | [Prompt Engineering](prompt-engineering.md) |
| Module Overview | [Module 11: Cheat Sheets](README.md) |

---

> **Tip:** Print this card and pin it next to your monitor. The first week of keyboard shortcuts feels slow, but it pays off within days.
