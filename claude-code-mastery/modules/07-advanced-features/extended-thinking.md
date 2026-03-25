# Extended Thinking & Adaptive Reasoning

**Module 07, Lesson 1 — Claude Code Mastery**

**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Overview

Extended thinking allows Claude to reason internally before producing a response. Instead of jumping straight to an answer, the model works through the problem step by step in a hidden "thinking" phase. This dramatically improves quality for complex tasks like architectural decisions, multi-file refactors, and debugging subtle issues. This lesson covers how to control thinking depth, when to use each level, and how to manage the associated cost.

---

## What Is Extended Thinking?

When extended thinking is active, Claude performs chain-of-thought reasoning before generating its visible response. The thinking tokens are consumed but not displayed by default. This mirrors how a senior engineer pauses to consider an approach before writing code.

| Aspect | Without Thinking | With Thinking |
|--------|-----------------|---------------|
| Response speed | Faster | Slower |
| Token usage | Lower | Higher |
| Quality on simple tasks | Equivalent | Equivalent |
| Quality on complex tasks | Lower | Significantly higher |
| Cost | Lower | Higher |

---

## Adaptive Reasoning

Models with adaptive reasoning — specifically **Opus 4.6** and **Sonnet 4.6** — automatically adjust their thinking depth based on task complexity. Simple questions get brief internal reasoning; complex problems get deep analysis.

To disable adaptive reasoning and force consistent thinking depth:

```bash
export CLAUDE_CODE_DISABLE_ADAPTIVE_THINKING=1
```

When disabled, the model uses the full thinking budget for every request regardless of complexity.

---

## The /effort Command

The `/effort` slash command controls how much reasoning Claude applies. Available levels:

| Level | Thinking Depth | Best For |
|-------|---------------|----------|
| `low` | Minimal reasoning | Simple edits, file reads, quick questions |
| `medium` | Moderate reasoning | Standard coding tasks, explanations |
| `high` | Deep reasoning | Complex refactors, architecture decisions |
| `max` | Maximum reasoning budget | Critical debugging, security audits |
| `auto` | Model decides (adaptive) | General use — recommended default |

Usage during a session:

```bash
> /effort high
# Now all responses use deep reasoning

> /effort auto
# Back to adaptive mode
```

---

## Keyboard Shortcuts

Toggle extended thinking on or off without leaving your conversation:

- **Alt+T** (Linux/Windows) — Toggle extended thinking
- **Option+T** (macOS) — Toggle extended thinking

To see the model's internal reasoning in the terminal:

- **Ctrl+O** — Toggle verbose mode, which displays thinking tokens in the output

Verbose mode is useful for understanding why Claude made a particular decision or for debugging unexpected behavior.

---

## Configuration Options

### settings.json

Set a persistent effort level in your project or user settings:

```json
{
  "effortLevel": "high"
}
```

Valid values: `"low"`, `"medium"`, `"high"`, `"max"`, `"auto"`.

### Environment Variable

Override effort level for a single session or in CI/CD:

```bash
export CLAUDE_CODE_EFFORT_LEVEL=max
claude -p "Audit this codebase for security vulnerabilities"
```

### Skill and Subagent Frontmatter

When creating custom skills, you can set effort in the frontmatter:

```markdown
---
effort: high
---
Perform a detailed code review of the staged changes.
```

This ensures the skill always runs at the specified reasoning depth regardless of the session default.

### MAX_THINKING_TOKENS

Control the upper bound on thinking tokens:

```bash
export MAX_THINKING_TOKENS=50000
```

This caps the number of tokens the model can use for internal reasoning. Lower values reduce cost but may truncate reasoning on complex tasks.

---

## Cost Considerations

Thinking tokens are billed at the same rate as output tokens. Higher effort levels consume more tokens per request.

| Effort Level | Approximate Token Multiplier |
|-------------|------------------------------|
| low | 1x baseline |
| medium | 2–3x baseline |
| high | 5–8x baseline |
| max | 10–15x baseline |

**Practical tips for cost control:**

- Use `auto` for daily work — the model skips heavy thinking on simple tasks
- Reserve `max` for critical decisions where correctness matters most
- Set `low` in CI pipelines that perform simple, repetitive tasks
- Use `MAX_THINKING_TOKENS` to set a hard ceiling in budget-sensitive environments
- Monitor token usage with `/cost` to track spending patterns

---

## When to Use Each Level

| Scenario | Recommended Effort |
|----------|--------------------|
| Renaming a variable across files | low |
| Writing a new utility function | medium |
| Designing a database schema | high |
| Debugging a race condition | high or max |
| Quick git status check | low |
| Security vulnerability audit | max |
| Everyday mixed work | auto |

---

## Priority Order

When multiple effort configurations exist, Claude Code resolves them in this order (highest priority first):

1. `/effort` command during session
2. `CLAUDE_CODE_EFFORT_LEVEL` environment variable
3. Skill/subagent frontmatter `effort` field
4. `effortLevel` in project `.claude/settings.json`
5. `effortLevel` in user `~/.claude/settings.json`
6. Default: `auto`

---

## Summary

Extended thinking is Claude Code's most direct quality lever. Adaptive reasoning in Opus 4.6 and Sonnet 4.6 handles most situations well, but manual control through `/effort`, environment variables, and settings gives you precision when it matters. Balance reasoning depth against cost, and use verbose mode to verify the model is thinking at the level you expect.

---

[← Back to Module Overview](README.md)

[← Previous Module](../06-hooks-mcp-commands/) | [Course Home](../../README.md) | [Next Module →](../08-multi-platform/)
