# Understanding AI Agents vs. Chatbots

**Module 01, Lesson 2 | Claude Cowork Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## The Key Difference

Understanding the difference between an **AI chatbot** and an **AI agent** is fundamental to getting the most out of Claude Cowork.

### AI Chatbot (What Most People Know)
- You ask a question → it gives a text answer
- It lives in a browser tab
- It cannot touch your files
- It cannot browse the web on its own
- Each conversation is isolated
- **You do the work** based on its suggestions

### AI Agent (What Cowork Is)
- You give a task → it **completes the task**
- It runs on your desktop with system access
- It can **read, create, and modify files**
- It can **browse the web** and bring back results
- It can chain multiple steps together
- **It does the work** while you supervise

---

## How Claude Cowork Acts as an Agent

When you give Cowork a task, it doesn't just respond with text. It creates an **action plan** and executes it:

### Example: "Organize my Downloads folder"

**A chatbot would say:**
> "Here are some tips for organizing your Downloads folder: Create subfolders for Documents, Images, and Videos..."

**Cowork actually does it:**
1. Scans your Downloads folder
2. Identifies file types (PDFs, images, spreadsheets, etc.)
3. Creates organized subfolders
4. Moves each file to the appropriate subfolder
5. Renames files with consistent naming conventions
6. Reports back what it did

---

## The Agent Loop

Cowork operates in a continuous **perception → planning → action** loop:

```
┌─────────────┐
│  1. PERCEIVE │ ← Reads your files, folders, or web pages
└──────┬──────┘
       │
┌──────▼──────┐
│  2. PLAN     │ ← Decides what steps to take
└──────┬──────┘
       │
┌──────▼──────┐
│  3. ACT      │ ← Creates files, moves data, browses web
└──────┬──────┘
       │
┌──────▼──────┐
│  4. REPORT   │ ← Tells you what was done
└─────────────┘
```

This loop can repeat multiple times within a single task, allowing Cowork to handle complex, multi-step workflows.

---

## What Makes Cowork Special

### 1. File System Access
Claude Cowork can interact with folders you designate on your computer. It can read documents, create spreadsheets, organize files, and more — all with your explicit permission.

### 2. Web Browsing
Cowork can go out onto the internet, research topics, find pricing data, analyze competitors, and bring back summarized reports.

### 3. Multi-Step Execution
Unlike chatbots that handle one exchange at a time, Cowork can execute complex workflows with dozens of steps — checking conditions, making decisions, and adapting along the way.

### 4. Memory & Context
Cowork maintains context across tasks, remembering your preferences, folder structures, and past instructions to become more effective over time.

---

## Safety & Permissions

An important thing to understand: **Cowork only accesses what you allow.**

- You explicitly grant access to specific folders
- It asks for confirmation before destructive actions
- You can revoke access at any time
- All actions are logged and reviewable

This is covered in detail in [Module 02: Folder Access](../02-cowork-fundamentals/folder-access.md).

---

## Key Takeaways

1. **Chatbots talk. Agents do.** Cowork executes tasks, not just answers questions.
2. **Cowork works with your actual files** — it's not a simulation.
3. **You stay in control** — Cowork operates within the permissions you set.
4. **Multi-step workflows** are where Cowork truly shines.

---

[← Previous Lesson](getting-started.md) | [Back to Module](README.md) | [Next Module →](../02-cowork-fundamentals/)
