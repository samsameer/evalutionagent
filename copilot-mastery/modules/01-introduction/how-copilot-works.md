# How Copilot Works Under the Hood

**Module 01, Lesson 3 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Understanding how GitHub Copilot generates code helps you write better prompts and get better suggestions. In this lesson, we explore the AI models, the context pipeline, and how Copilot turns your intent into working code.

---

## The AI Models Behind Copilot

GitHub Copilot is powered by **multiple Large Language Models (LLMs)**. As of March 2026, you can choose from:

| Model | Provider | Best For | Availability |
|-------|----------|----------|-------------|
| **GPT-4o** | OpenAI | General coding, fast completions | All plans (default) |
| **Claude 3.5 Sonnet** | Anthropic | Nuanced explanations, careful reasoning | Free, Pro, Pro+, Business, Enterprise |
| **Claude 3.7 Sonnet** | Anthropic | Extended thinking, complex problem solving | Pro+, Enterprise |
| **Gemini 2.0 Flash** | Google | Fast responses, multimodal | Pro, Pro+, Business, Enterprise |
| **Gemini 2.5 Pro** | Google | Advanced reasoning, long context | Pro+, Enterprise |
| **o1** | OpenAI | Deep reasoning, math, algorithms | Pro+ (premium), Enterprise (premium) |
| **o3-mini** | OpenAI | Reasoning with faster responses | Pro+ (premium), Enterprise (premium) |

### How to Switch Models

In VS Code Copilot Chat, click the **model selector** dropdown at the top of the chat panel to switch between available models. Different models may give different quality responses depending on the task.

---

## The Context Pipeline

When you type code, Copilot does not just look at the current line. It builds a **rich context** from multiple sources:

```
┌──────────────────────────────────────────────────┐
│              Context Pipeline                      │
├──────────────────────────────────────────────────┤
│                                                    │
│  1. Current File                                   │
│     └─ The file you are editing (full content)    │
│                                                    │
│  2. Open Tabs                                      │
│     └─ Other files open in your editor            │
│                                                    │
│  3. Neighboring Files                              │
│     └─ Related files in same directory            │
│                                                    │
│  4. Project Structure                              │
│     └─ File tree, package.json, imports           │
│                                                    │
│  5. Language & Framework                           │
│     └─ Detected language, framework patterns      │
│                                                    │
│  6. Comments & Docstrings                          │
│     └─ Your comments describing intent            │
│                                                    │
│  7. Custom Instructions                            │
│     └─ .github/copilot-instructions.md            │
│                                                    │
│  8. Chat History (for Chat)                        │
│     └─ Previous messages in conversation          │
│                                                    │
└──────────────────────────────────────────────────┘
                    │
                    ▼
           ┌──────────────┐
           │   LLM Model  │
           │  (GPT-4o,    │
           │   Claude,    │
           │   Gemini)    │
           └──────────────┘
                    │
                    ▼
           ┌──────────────┐
           │  Suggestion  │
           │  (Ghost Text │
           │   or Chat    │
           │   Response)  │
           └──────────────┘
```

### Why This Matters

The more context Copilot has, the better its suggestions. This is why:

- **Keeping related files open** in tabs improves suggestions
- **Writing clear comments** before a function gives Copilot intent
- **Using descriptive variable names** helps Copilot understand your code
- **Having a well-structured project** enables better cross-file understanding

---

## How Code Completions Work

1. **You type code** in your editor
2. **Copilot extension** captures the cursor position and surrounding context
3. **Context is sent** to GitHub's servers (encrypted in transit)
4. **The LLM processes** the context and generates a completion
5. **The suggestion appears** as ghost text in your editor
6. **You accept (Tab)** or dismiss (Escape) the suggestion

### Latency and Performance

- Suggestions typically appear in **100-500 milliseconds**
- Copilot uses **speculative decoding** for faster completions
- Local caching prevents redundant API calls
- The extension throttles requests to avoid overwhelming the model

---

## How Copilot Chat Works

1. **You type a question** in the chat panel (or inline with `Ctrl+I`)
2. **Copilot gathers context** — your selection, open file, workspace structure
3. **Context variables** (like `#file`, `#selection`) add specific references
4. **Chat participants** (like `@workspace`, `@terminal`) expand the scope
5. **The LLM generates** a response with code, explanations, or actions
6. **You apply, copy,** or ask follow-up questions

---

## How Agent Mode Works

Agent mode is fundamentally different from completions and chat:

1. **You describe a task** (e.g., "Add user authentication to this app")
2. **Copilot plans** the implementation — identifying files to create/modify
3. **It edits files** autonomously, potentially creating new ones
4. **It runs terminal commands** (build, test, lint) to validate its work
5. **If errors occur**, it reads the output and fixes them automatically
6. **It iterates** until the task is complete or it needs your input
7. **You review** the changes and accept or provide feedback

### The Agentic Loop

```
  Describe Task
       │
       ▼
  ┌─────────┐
  │  Plan    │◄──────────────┐
  └────┬─────┘               │
       │                     │
       ▼                     │
  ┌─────────┐               │
  │  Edit    │               │
  │  Files   │               │
  └────┬─────┘               │
       │                     │
       ▼                     │
  ┌─────────┐    Error?     │
  │  Run     │──── Yes ──────┘
  │  Commands│
  └────┬─────┘
       │ No Error
       ▼
  ┌─────────┐
  │  Done!   │
  │  Review  │
  └──────────┘
```

---

## Data Privacy — What Gets Sent?

This is a common concern. Here is what happens with your code:

### For Individual Plans (Free, Pro, Pro+)

- **Prompts and suggestions** are sent to GitHub's servers for processing
- **Code snippets** (context from your editor) are transmitted encrypted
- As of 2024, GitHub **does not use your code to train models** (opt-out by default)
- Suggestions are **not stored** after being generated

### For Business and Enterprise Plans

- **No code is retained** for training — ever
- **Content exclusions** can prevent specific files from being sent
- **Audit logs** track all Copilot interactions
- Data is processed in compliance with your organization's data residency requirements

> **Key Point:** Your code is used only to generate suggestions in real-time. It is not stored or used to improve the model.

---

## Code Referencing and Public Code Matching

Copilot includes a **code referencing** feature that detects when a suggestion closely matches publicly available code on GitHub. When this happens:

- The suggestion is flagged with the **source repository** and **license**
- You can decide whether to use the code based on its license
- Business and Enterprise plans can **block suggestions** that match public code

This feature protects you from accidentally including code with incompatible licenses in your project.

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 01: Introduction](README.md) |
| Previous Lesson | [Plans, Pricing & Feature Comparison](plans-and-pricing.md) |
| Next Module | [Module 02: Setup & Installation](../02-setup-installation/) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
