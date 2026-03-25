# Plans, Pricing & Model Comparison

**Module 01, Lesson 2 — Claude Code Mastery**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Claude Code is available through several Anthropic subscription plans, each offering different levels of usage, models, and features. This lesson breaks down every option so you can choose the right one.

---

## Subscription Plans

| Plan | Price | Claude Code Access | Models Available | Best For |
|------|-------|-------------------|-----------------|----------|
| **Claude Pro** | $20/month | Yes | Sonnet 4.6, Haiku 4.5 | Individual developers on a budget |
| **Claude Max (5x)** | $100/month | Yes | Opus 4.6, Sonnet 4.6, Haiku 4.5 | Power users who need Opus |
| **Claude Max (20x)** | $200/month | Yes | Opus 4.6, Sonnet 4.6, Haiku 4.5 | Heavy daily users |
| **Claude Team** | $30/user/month | Yes | Opus 4.6, Sonnet 4.6, Haiku 4.5 | Small to medium teams |
| **Claude Enterprise** | Custom pricing | Yes | All models + custom routing | Large organizations |
| **API (Pay-as-you-go)** | Per token | Yes | All models | Developers who prefer usage-based billing |

### Plan Features Comparison

| Feature | Pro | Max | Team | Enterprise | API |
|---------|-----|-----|------|-----------|-----|
| Claude Code CLI | Yes | Yes | Yes | Yes | Yes |
| VS Code Extension | Yes | Yes | Yes | Yes | Yes |
| JetBrains Extension | Yes | Yes | Yes | Yes | Yes |
| Claude Code Web | Yes | Yes | Yes | Yes | No |
| Desktop App | Yes | Yes | Yes | Yes | No |
| Opus 4.6 Model | Limited | Yes | Yes (Premium) | Yes | Yes |
| 1M Token Context | Extra usage | Included | Extra usage | Included | Yes |
| Auto Mode | No | No | Yes | Yes | No |
| Managed Policies | No | No | No | Yes | No |
| SSO/SCIM | No | No | No | Yes | No |
| Code Review Service | No | No | Yes | Yes | No |

---

## AI Models Powering Claude Code

### Claude Opus 4.6

- **Alias:** `opus`
- **Best for:** Complex reasoning, multi-file refactors, architectural decisions
- **Context:** 200K standard, 1M extended
- **Speed:** Slower but most capable
- **Cost:** Highest token cost
- **Features:** Adaptive reasoning with configurable effort levels

### Claude Sonnet 4.6

- **Alias:** `sonnet`
- **Best for:** Most daily coding tasks — balanced speed and quality
- **Context:** 200K standard, 1M extended
- **Speed:** Fast with strong capabilities
- **Cost:** Moderate token cost
- **Features:** Adaptive reasoning, excellent code generation

### Claude Haiku 4.5

- **Alias:** `haiku`
- **Best for:** Simple tasks, quick questions, subagent operations
- **Context:** 200K
- **Speed:** Fastest
- **Cost:** Lowest token cost
- **Features:** Best for high-volume, low-complexity tasks

### Model Aliases

| Alias | What It Maps To |
|-------|----------------|
| `default` | Auto-selected based on your plan |
| `sonnet` | Latest Claude Sonnet 4.6 |
| `opus` | Latest Claude Opus 4.6 |
| `haiku` | Latest Claude Haiku 4.5 |
| `sonnet[1m]` | Sonnet with 1M token context |
| `opus[1m]` | Opus with 1M token context |
| `opusplan` | Opus for planning, Sonnet for execution |

---

## Average Cost Estimates (API Users)

| Metric | Typical Cost |
|--------|-------------|
| Per developer per day | ~$6 |
| Per developer per month | $100-200 (Sonnet) |
| 90th percentile daily cost | <$12 |
| Per code review | $15-25 |

> **Tip:** Pro subscribers don't pay per-token — your usage is covered by the subscription. API users pay per token and should monitor with `/cost`.

---

## Choosing the Right Plan

**Choose Pro if:**
- You're an individual developer
- Sonnet 4.6 meets your needs (it does for most tasks)
- You have moderate daily usage

**Choose Max if:**
- You need Opus 4.6 for complex reasoning
- You use Claude Code heavily throughout the day
- You want 1M context included

**Choose Team if:**
- You have a development team of 2+
- You want centralized billing and usage monitoring
- You need auto mode for reduced permission prompts

**Choose Enterprise if:**
- You need SSO, SCIM, managed policies
- You require custom model routing (Bedrock, Vertex)
- You need organization-wide compliance controls

**Choose API if:**
- You prefer pay-as-you-go billing
- You're building automation with headless mode
- You want full control over model selection and parameters

---

**Next:** [Architecture — How Claude Code Works](architecture.md)

[← Back to Module Overview](README.md) | [Next Module: Installation & Setup →](../02-installation-setup/)

---

*Module 01, Lesson 2 — Claude Code Mastery — March 2026*
