# Module 01: Introduction to GitHub Copilot

**GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Module Overview

GitHub Copilot is the world's most widely adopted AI coding assistant, integrated directly into your development environment. But what exactly is it? How does it work? And what plan should you choose?

In this module, we start from the very beginning. You will learn what GitHub Copilot is, how it differs from traditional autocomplete, what AI models power it, and how to choose the right plan for your needs. By the end of this module, you will have a solid foundation to build upon in the rest of the course.

---

## Learning Objectives

- Understand what GitHub Copilot is and its evolution from 2021 to 2026
- Learn the difference between code completion, Copilot Chat, agent mode, and the Coding Agent
- Compare all Copilot plans and choose the right one for your needs
- Understand the AI models (GPT-4o, Claude 3.5/4, Gemini, o1, o3-mini) powering Copilot

---

## Lessons

| Lesson | Topic | Description |
|--------|-------|-------------|
| 1 | [What is GitHub Copilot?](README.md) | This page — overview and history |
| 2 | [Plans, Pricing & Feature Comparison](plans-and-pricing.md) | Free, Pro, Pro+, Business, Enterprise breakdown |
| 3 | [How Copilot Works Under the Hood](how-copilot-works.md) | LLMs, context windows, and code generation |

---

## What is GitHub Copilot?

GitHub Copilot is an **AI-powered coding assistant** developed by GitHub (Microsoft) that integrates directly into your code editor, terminal, and the GitHub platform itself. It uses large language models (LLMs) to:

- **Suggest code as you type** — Inline completions that appear as ghost text
- **Answer coding questions** — Via Copilot Chat in your editor or on GitHub.com
- **Edit multiple files at once** — Through Copilot Edits
- **Autonomously complete tasks** — Via Agent Mode and the Copilot Coding Agent
- **Explain and suggest terminal commands** — Through the Copilot CLI
- **Summarize pull requests** — Automatically generate PR descriptions
- **Review code** — AI-powered code review on GitHub.com

### A Brief History

| Year | Milestone |
|------|-----------|
| June 2021 | GitHub Copilot launched as a technical preview |
| June 2022 | Copilot became generally available ($10/month for individuals) |
| February 2023 | Copilot for Business launched |
| November 2023 | Copilot Chat became generally available |
| February 2024 | Copilot Enterprise launched with knowledge bases |
| September 2024 | Copilot Extensions launched |
| October 2024 | Multi-model support added (Claude, Gemini alongside GPT-4o) |
| December 2024 | GitHub Copilot Free tier launched (2,000 completions/month) |
| February 2025 | Agent Mode launched in VS Code (preview) |
| May 2025 | Copilot Coding Agent launched (assigns issues to Copilot) |
| June 2025 | MCP support added to agent mode |
| October 2025 | Copilot Coding Agent became generally available |
| January 2026 | Next Edit Suggestions (NES) generally available |
| March 2026 | Vision capabilities, expanded model selection, enhanced agent mode |

---

## The Four Pillars of GitHub Copilot

```
┌─────────────────────────────────────────────────────────────────┐
│                    GitHub Copilot Ecosystem                      │
├────────────────┬────────────────┬──────────────┬────────────────┤
│  Code          │  Copilot       │  Agent        │  Coding        │
│  Completions   │  Chat          │  Mode         │  Agent         │
├────────────────┼────────────────┼──────────────┼────────────────┤
│ Inline ghost   │ Q&A about      │ Autonomous   │ Assign GitHub  │
│ text as you    │ code, explain, │ multi-step   │ Issues to      │
│ type. Tab to   │ fix, test,     │ task runner   │ Copilot. It    │
│ accept.        │ document.      │ in your       │ creates PRs    │
│                │                │ editor.       │ autonomously.  │
├────────────────┼────────────────┼──────────────┼────────────────┤
│ Available in:  │ Available in:  │ Available in:│ Available on:  │
│ VS Code        │ VS Code        │ VS Code      │ GitHub.com     │
│ JetBrains      │ JetBrains      │              │                │
│ Neovim         │ GitHub.com     │              │                │
│ Xcode          │ CLI            │              │                │
└────────────────┴────────────────┴──────────────┴────────────────┘
```

### 1. Code Completions (The Foundation)

This is where Copilot started. As you type code, Copilot shows **ghost text** — semi-transparent suggestions that appear inline. Press **Tab** to accept the full suggestion, or use **Ctrl+Right Arrow** to accept word by word.

Copilot does not just autocomplete variable names — it can generate entire functions, classes, test suites, and algorithms based on the context of your file, your open tabs, and your project structure.

### 2. Copilot Chat (The Conversationalist)

Copilot Chat lets you have a natural language conversation about your code. You can:

- Ask **"What does this function do?"** and get a detailed explanation
- Say **"Write tests for this class"** and get a full test suite
- Request **"Fix this bug"** and get corrected code
- Ask about your entire workspace with `@workspace`

### 3. Agent Mode (The Autonomous Worker)

Agent mode takes Copilot from a suggestion engine to an **autonomous coding agent**. When you give it a task in agent mode, it can:

- Plan the implementation across multiple files
- Create new files and edit existing ones
- Run terminal commands (build, test, lint)
- Read command output and fix errors automatically
- Install packages and dependencies
- Use MCP tools to interact with external services

### 4. Copilot Coding Agent (The Autonomous Developer)

The most advanced capability — you can **assign a GitHub Issue to Copilot** and it will:

- Analyze the issue and plan the implementation
- Create a branch and write the code
- Run tests and fix failures
- Open a pull request with a summary
- Respond to review feedback

---

## Prerequisites

Before diving into the rest of the course, ensure you have:

- [ ] A GitHub account (free or paid)
- [ ] A code editor (VS Code recommended, but JetBrains, Neovim, and Xcode are also supported)
- [ ] Basic familiarity with writing code in at least one programming language
- [ ] A desire to 10x your development productivity

---

## Navigation

| Direction | Link |
|-----------|------|
| Course Home | [GitHub Copilot Mastery](../../README.md) |
| Next Module | [Module 02: Setup & Installation](../02-setup-installation/) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
