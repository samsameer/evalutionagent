# Chat Modes — Inline, Panel & Quick Chat

**Module 04, Lesson 1 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Copilot Chat in VS Code offers **three distinct modes** for interacting with the AI. Each mode is optimized for different use cases. Choosing the right mode for the right situation is key to an efficient workflow.

---

## The Three Chat Modes

```
┌─────────────────────────────────────────────────────────────┐
│                   Copilot Chat Modes                         │
├──────────────────┬──────────────────┬───────────────────────┤
│   Chat Panel     │   Inline Chat    │   Quick Chat          │
├──────────────────┼──────────────────┼───────────────────────┤
│ Sidebar panel    │ Appears at       │ Floating dialog       │
│ for extended     │ cursor position  │ at top of editor      │
│ conversations    │ for quick edits  │ for fast questions    │
├──────────────────┼──────────────────┼───────────────────────┤
│ Ctrl+Alt+I       │ Ctrl+I           │ Ctrl+Shift+I          │
│ Cmd+Option+I     │ Cmd+I            │ Cmd+Shift+I           │
└──────────────────┴──────────────────┴───────────────────────┘
```

---

## 1. Chat Panel (Sidebar)

### How to Open
- **Shortcut:** `Ctrl+Alt+I` (Windows/Linux) or `Cmd+Option+I` (macOS)
- **Command Palette:** "GitHub Copilot: Open Chat"
- **Click:** The Copilot icon in the activity bar (left sidebar)

### Best For
- Extended, multi-turn conversations
- Researching code architecture
- Planning implementations
- Asking broad questions about your workspace
- Learning and exploration

### Features
- **Persistent conversation history** within the session
- **Model selector** at the top to switch between GPT-4o, Claude, Gemini, etc.
- **Mode selector** to switch between Ask, Edit, and Agent modes
- **File references** — drag files into chat or use #file
- **Code blocks** with copy/apply buttons
- **Follow-up questions** — continue the conversation with context

### Example Conversation

```
You: @workspace How is authentication implemented in this project?

Copilot: Based on the codebase, authentication is implemented using JWT tokens...
  - `src/auth/auth.service.ts` handles token generation
  - `src/middleware/auth.middleware.ts` validates tokens on each request
  - `src/auth/strategies/` contains OAuth providers (Google, GitHub)
  ...

You: Can you show me how to add Apple Sign-In as a new strategy?

Copilot: Here's how to add Apple Sign-In...
```

---

## 2. Inline Chat

### How to Open
- **Shortcut:** `Ctrl+I` (Windows/Linux) or `Cmd+I` (macOS)
- Place your cursor where you want the edit, then press the shortcut

### Best For
- Quick code edits at the cursor position
- Generating code in a specific location
- Fixing a bug on a specific line
- Adding a specific piece of code inline

### Features
- **Appears directly in the editor** at your cursor position
- **Shows diff preview** — you see exactly what will change before accepting
- **Accept/Discard buttons** — review changes before they are applied
- **Minimal context switching** — you stay in your code flow

### Example Usage

1. Select a block of code
2. Press `Ctrl+I`
3. Type: "Add error handling with try-catch"
4. Review the diff preview
5. Click **Accept** or press `Ctrl+Enter`

### Inline Chat with Selection

If you **select code before pressing `Ctrl+I`**, Copilot knows exactly what code you want to modify:

```python
# Select these lines:
def process_data(data):
    result = transform(data)
    return result

# Press Ctrl+I and type: "Add input validation and logging"
```

Copilot modifies only the selected code, showing a diff you can accept or reject.

---

## 3. Quick Chat

### How to Open
- **Shortcut:** `Ctrl+Shift+I` (Windows/Linux) or `Cmd+Shift+I` (macOS)

### Best For
- Fast, one-off questions
- Quick lookups ("What's the syntax for...?")
- Brief code generation
- When you do not want to leave your current editor view

### Features
- **Floating dialog** at the top of the editor
- **Disappears after use** — does not persist in sidebar
- **Lightweight** — opens and closes instantly
- Can be promoted to full chat panel if the conversation grows

---

## Choosing the Right Mode

| Scenario | Recommended Mode |
|----------|-----------------|
| "What does this project do?" | **Chat Panel** — extended answer needed |
| "Fix this function" | **Inline Chat** — edit at cursor |
| "What's the syntax for async/await in Rust?" | **Quick Chat** — fast answer |
| "Refactor this entire module" | **Chat Panel** with Agent mode |
| "Add a comment to this line" | **Inline Chat** — precise location |
| "How do I run tests in this project?" | **Quick Chat** — quick lookup |
| "Build a new feature across multiple files" | **Chat Panel** with Agent mode |

---

## Chat Panel Modes (Ask, Edit, Agent)

The Chat Panel has three sub-modes accessible via the **mode selector** at the top:

### Ask Mode
- Default mode — ask questions, get explanations
- Does not modify your files
- Great for learning and exploration

### Edit Mode (Copilot Edits)
- Direct file editing through conversation
- Shows diffs you can accept or reject
- Can work across multiple files
- Covered in depth in [Module 05](../05-copilot-edits-agent-mode/)

### Agent Mode
- Autonomous task execution
- Can create files, run commands, install packages
- Iterates until the task is complete
- Covered in depth in [Module 05](../05-copilot-edits-agent-mode/)

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 04: Copilot Chat](README.md) |
| Next Lesson | [Chat Participants & Slash Commands](participants-and-commands.md) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
