# Model Selection & Switching

**Module 10, Lesson 2 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

GitHub Copilot supports **multiple AI models** from different providers. Choosing the right model for the right task can significantly improve the quality, speed, and cost-efficiency of your interactions.

---

## Available Models (March 2026)

| Model | Provider | Speed | Reasoning | Best For | Plan Required |
|-------|----------|-------|-----------|----------|--------------|
| **GPT-4o** | OpenAI | Fast | Good | General coding, fast completions | All plans |
| **Claude 3.5 Sonnet** | Anthropic | Fast | Very Good | Explanations, careful coding | All plans |
| **Claude 3.7 Sonnet** | Anthropic | Medium | Excellent | Complex problems, extended thinking | Pro+, Enterprise |
| **Gemini 2.0 Flash** | Google | Very Fast | Good | Quick tasks, multimodal | Pro, Pro+, Business, Enterprise |
| **Gemini 2.5 Pro** | Google | Medium | Very Good | Long context, complex analysis | Pro+, Enterprise |
| **o1** | OpenAI | Slow | Exceptional | Algorithms, math, deep reasoning | Pro+ (premium), Enterprise (premium) |
| **o3-mini** | OpenAI | Medium | Excellent | Reasoning with better speed than o1 | Pro+ (premium), Enterprise (premium) |

---

## How to Switch Models

### In Copilot Chat (VS Code)

1. Open Copilot Chat panel
2. Look at the **top of the chat panel** for the model name
3. Click the **model dropdown**
4. Select your desired model
5. All subsequent messages use the new model

### In Inline Chat

The inline chat uses the same model selected in the main chat panel.

### In Agent Mode

Agent mode uses the selected model. For complex tasks, consider switching to Claude 3.7 Sonnet or o1 for better reasoning.

---

## Model Selection Guide

### Choose **GPT-4o** When:
- You want the **fastest responses**
- Writing standard code (CRUD, boilerplate, common patterns)
- Working with code completions (inline ghost text)
- The task is straightforward and does not need deep reasoning

### Choose **Claude 3.5 Sonnet** When:
- You want **careful, detailed explanations**
- Working on code review or refactoring
- You need nuanced understanding of complex code
- Writing documentation or comments

### Choose **Claude 3.7 Sonnet** When:
- The problem is **complex and requires extended thinking**
- Debugging subtle issues
- Architectural decisions
- Implementing complex algorithms with edge cases

### Choose **Gemini 2.0 Flash** When:
- You need **very fast responses**
- Working with **images** (vision tasks)
- Quick question-and-answer sessions
- You have a large codebase and need fast context processing

### Choose **Gemini 2.5 Pro** When:
- Working with **very long files** or extensive context
- Complex analysis across many files
- Tasks that benefit from Google's large context window

### Choose **o1 or o3-mini** When:
- **Deep reasoning** is critical (algorithms, mathematical proofs)
- Debugging extremely subtle logic errors
- Optimizing complex algorithms
- Solving competitive programming-style problems

> **Note:** o1 and o3-mini consume **premium requests**. Use them deliberately for tasks that truly need deep reasoning.

---

## Model Comparison: Same Task, Different Models

### Task: "Implement a rate limiter using the sliding window algorithm"

| Model | Approach |
|-------|----------|
| **GPT-4o** | Quick implementation, functional, may miss edge cases |
| **Claude 3.5 Sonnet** | Well-explained, handles edge cases, clear code |
| **o1** | Deep analysis of algorithmic tradeoffs, optimal implementation, proves correctness |

---

## Cost Implications

| Model Type | Cost Impact |
|-----------|------------|
| Standard models (GPT-4o, Claude 3.5 Sonnet) | No additional cost beyond subscription |
| Premium models (o1, o3-mini) | Consumes premium requests from monthly allowance |
| Fast models (Gemini Flash) | No additional cost |

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 10: Advanced Features](README.md) |
| Previous Lesson | [Custom Instructions](custom-instructions.md) |
| Next Lesson | [Prompt Files & Reusable Prompts](prompt-files.md) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
