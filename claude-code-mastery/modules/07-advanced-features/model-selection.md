# Model Selection & Configuration

**Module 07, Lesson 2 — Claude Code Mastery**

**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Overview

Claude Code supports multiple models, each with different capabilities, context sizes, and cost profiles. Choosing the right model for a task can dramatically improve both quality and efficiency. This lesson covers the available models, how to switch between them, and how organizations can control model access.

---

## Available Models

| Model ID | Description | Context Window | Strengths |
|----------|-------------|----------------|-----------|
| `opus` | Claude Opus — most capable | 200K tokens | Complex reasoning, architecture, debugging |
| `sonnet` | Claude Sonnet — balanced | 200K tokens | General coding, fast responses, cost-effective |
| `haiku` | Claude Haiku — fastest | 200K tokens | Simple tasks, quick lookups, high throughput |
| `opus[1m]` | Claude Opus — extended context | 1M tokens | Large codebase analysis, massive refactors |
| `sonnet[1m]` | Claude Sonnet — extended context | 1M tokens | Large file reviews, broad search tasks |
| `opusplan` | Opus with planning mode | 200K tokens | Multi-step projects, coordinated changes |

---

## Selecting a Model

### The /model Command

During an interactive session, use the `/model` command to open an interactive picker:

```bash
> /model
# Opens a model selection menu with an effort slider
# Use arrow keys to navigate, Enter to confirm
```

The picker displays available models and lets you adjust the effort level simultaneously.

### The --model Startup Flag

Set the model when launching Claude Code:

```bash
claude --model opus[1m]
claude --model sonnet
claude --model haiku
```

### ANTHROPIC_MODEL Environment Variable

Set a default model for all sessions:

```bash
export ANTHROPIC_MODEL=opus
claude
```

### settings.json

Persist the model choice in your settings file:

```json
{
  "model": "sonnet"
}
```

This can be set at user level (`~/.claude/settings.json`) or project level (`.claude/settings.json`).

---

## Priority Order

When multiple model configurations exist, Claude Code resolves them as follows (highest priority first):

1. `/model` command during session
2. `--model` flag at startup
3. `ANTHROPIC_MODEL` environment variable
4. `model` in project `.claude/settings.json`
5. `model` in user `~/.claude/settings.json`
6. Default model (varies by plan)

---

## 1M Context Windows

The extended context models (`opus[1m]` and `sonnet[1m]`) provide 1 million tokens of context. This is essential for tasks that involve reading many files or working with very large codebases.

**Availability by plan:**

| Plan | opus[1m] | sonnet[1m] |
|------|----------|------------|
| Free | No | No |
| Pro | Limited | Yes |
| Team | Yes | Yes |
| Enterprise | Yes | Yes |

When you need 1M context:

- Analyzing a full microservices repository in one session
- Reviewing hundreds of test files for patterns
- Performing codebase-wide refactors with full awareness
- Reading and summarizing large documentation sets

---

## Custom Model Options

For specialized deployments, use the `ANTHROPIC_CUSTOM_MODEL_OPTION` environment variable to register additional model choices:

```bash
export ANTHROPIC_CUSTOM_MODEL_OPTION="my-fine-tuned-model:My Custom Model:200000"
```

The format is `model_id:display_name:context_window`. Custom models then appear in the `/model` picker alongside the built-in options.

---

## Enterprise Model Controls

Organizations can restrict and override model access using managed settings.

### modelOverrides

Administrators can remap model identifiers to specific versions or deployments:

```json
{
  "modelOverrides": {
    "opus": "claude-opus-4-20260301",
    "sonnet": "claude-sonnet-4-20260301"
  }
}
```

This ensures all users on a team use the same model version, which is important for reproducibility and compliance.

### availableModels

Restrict which models users can select:

```json
{
  "availableModels": ["sonnet", "haiku"]
}
```

When this is set, users cannot switch to models outside the list. The `/model` picker only shows allowed options. This is useful for:

- Controlling costs by disabling Opus on budget-constrained teams
- Enforcing specific models for compliance or audit requirements
- Standardizing the team experience

---

## Choosing the Right Model

| Task | Recommended Model | Reason |
|------|-------------------|--------|
| Quick code edits | haiku | Fast, cheap |
| Standard development | sonnet | Balanced quality and speed |
| Complex architecture | opus | Deepest reasoning |
| Large codebase analysis | sonnet[1m] or opus[1m] | Needs broad context |
| Multi-step project planning | opusplan | Coordinated planning |
| CI/CD automation | sonnet or haiku | Cost-effective at scale |
| Security audit | opus | Maximum thoroughness |

---

## Practical Workflow

A common pattern is to start with a fast model and escalate when needed:

```bash
# Start with Sonnet for everyday work
claude --model sonnet

# Switch to Opus mid-session for a hard problem
> /model opus

# Drop to Haiku for bulk file operations
> /model haiku
```

This keeps costs low while ensuring you have full reasoning power when it matters.

---

## Summary

Model selection is a lever for balancing speed, quality, and cost. Use Haiku for fast tasks, Sonnet for daily work, and Opus for complex reasoning. Extended 1M context models unlock large-codebase workflows. Enterprise controls through `modelOverrides` and `availableModels` let organizations standardize and manage model access across teams.

---

[← Back to Module Overview](README.md)

[← Previous Module](../06-hooks-mcp-commands/) | [Course Home](../../README.md) | [Next Module →](../08-multi-platform/)
