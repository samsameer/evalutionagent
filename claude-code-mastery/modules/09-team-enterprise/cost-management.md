# Cost Management & Monitoring

**Module 09, Lesson 3 — Claude Code Mastery**

**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Overview

Claude Code costs scale with team size and usage intensity. This lesson covers real-world cost benchmarks, monitoring tools, spend limits, rate limit recommendations, and practical strategies for reducing costs without sacrificing productivity. Understanding these levers lets engineering managers budget accurately and optimize spend over time.

---

## Average Costs per Developer

Based on typical usage patterns across engineering teams:

| Usage Level | Daily Cost | Monthly Cost | Profile |
|-------------|-----------|--------------|---------|
| Light | ~$3/day | $50–80/month | Occasional prompts, small context |
| Average | ~$6/day | $100–200/month | Regular daily use, medium projects |
| Heavy | ~$12/day | $250–400/month | Continuous use, large codebases, Opus model |

These figures assume API billing. Pro plan users pay a flat subscription instead.

---

## The /cost Command

API users can check their current session spend at any time:

```json
// In any Claude Code session, type:
// /cost
//
// Output:
// Session cost: $1.47
// ├─ Input tokens:  142,000 ($0.43)
// ├─ Output tokens:  38,000 ($0.57)
// └─ Cache reads:    95,000 ($0.10)
```

The `/cost` command shows a breakdown by token type so you can identify what is driving spend — large context windows, verbose outputs, or cache misses.

---

## Workspace Spend Limits

Organizations can set spend limits at the workspace level to prevent runaway costs:

| Limit Type | Scope | Effect When Reached |
|-----------|-------|---------------------|
| Hard limit | Per workspace | API calls blocked until next billing period |
| Soft limit | Per workspace | Alert sent to admins, usage continues |
| Per-user limit | Individual developer | Developer notified, must request increase |

Configure spend limits through the Anthropic Console under workspace settings. Set alerts at 50%, 75%, and 90% thresholds to catch unexpected spikes early.

---

## Rate Limit Recommendations by Team Size

Rate limits prevent individual users or teams from consuming disproportionate API capacity:

| Team Size | Recommended TPM | Recommended RPM | Notes |
|-----------|----------------|-----------------|-------|
| 1–5 devs | 400,000 | 200 | Default tier is usually sufficient |
| 6–20 devs | 1,000,000 | 500 | Request tier increase proactively |
| 21–50 devs | 4,000,000 | 2,000 | Coordinate with Anthropic account team |
| 50+ devs | Custom | Custom | Enterprise agreement recommended |

| Term | Definition |
|------|-----------|
| TPM | Tokens per minute — total input + output tokens consumed |
| RPM | Requests per minute — number of API calls made |

Request rate limit increases before onboarding large groups. Running into limits mid-sprint disrupts developer flow.

---

## Reducing Costs: Model Selection

The single biggest cost lever is model choice:

| Model | Input Cost (per 1M tokens) | Output Cost (per 1M tokens) | Best For |
|-------|---------------------------|----------------------------|----------|
| Haiku 3.5 | $0.80 | $4.00 | Quick edits, simple tasks |
| Sonnet 4 | $3.00 | $15.00 | Daily development, balanced quality/cost |
| Opus 4 | $15.00 | $75.00 | Complex architecture, difficult debugging |

Use `/model` to switch models within a session. Start with Sonnet for most tasks and escalate to Opus only for genuinely complex problems.

---

## Reducing Costs: Context Management

Large context windows drive token costs up. Keep context lean:

| Strategy | How | Impact |
|----------|-----|--------|
| Use `/compact` regularly | Summarizes conversation, drops old context | Reduces input tokens by 50–80% |
| Start new sessions | Fresh context for unrelated tasks | Eliminates accumulated bloat |
| Scope your requests | Ask about specific files, not "the whole project" | Fewer files read into context |
| Use `.claudeignore` | Exclude build artifacts, vendor directories | Prevents unnecessary file reads |

---

## Reducing Costs: Thinking Effort

Control how much reasoning Claude does before responding:

```json
// Set via environment variable or settings
// CLAUDE_THINKING_EFFORT=low   (fastest, cheapest)
// CLAUDE_THINKING_EFFORT=medium (balanced)
// CLAUDE_THINKING_EFFORT=high   (most thorough, most expensive)
```

Lower thinking effort reduces output tokens from the extended thinking process. Use `low` for routine tasks and `high` only when debugging complex issues.

---

## MCP Overhead and Subagent Costs

MCP servers and subagents add to total cost because each tool call and subagent invocation consumes additional tokens:

| Cost Factor | Description | Mitigation |
|-------------|-------------|------------|
| MCP tool descriptions | Each server's tool schema is included in context | Limit connected MCP servers to those actively needed |
| Subagent spawning | Each subagent gets its own context window | Avoid unnecessary parallel subagents |
| Tool call overhead | Each call adds request/response tokens | Batch related operations where possible |
| Recursive agents | Subagents spawning subagents | Set max depth limits in configuration |

Disconnect MCP servers you are not actively using. Each connected server adds its tool definitions to every API call, even if the tools are never invoked.

---

## Cost Optimization Checklist

| Action | Expected Savings |
|--------|-----------------|
| Default to Sonnet instead of Opus | 60–80% per token |
| Run `/compact` every 15–20 exchanges | 50–80% context reduction |
| Set thinking effort to medium | 20–40% on output tokens |
| Disconnect unused MCP servers | 5–15% on input tokens |
| Use content exclusions for large directories | 10–30% on file reads |
| Start fresh sessions for new tasks | Eliminates context bloat |

---

## Navigation

| Direction | Link |
|-----------|------|
| Previous | [Enterprise Configuration](enterprise-config.md) |
| Next | [Security, Privacy & Compliance](security-privacy.md) |
| Module Home | [Module 09: Team & Enterprise](README.md) |
