# Metrics & Usage Analytics

**Module 11, Lesson 5 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

For organizations investing in Copilot, measuring its impact is essential. The Copilot Metrics dashboard provides detailed usage analytics, adoption trends, and productivity indicators.

---

## Accessing Metrics

### Organization Level

1. Go to **Organization Settings** → **Copilot** → **Metrics**
2. View the analytics dashboard

### Enterprise Level

Enterprise admins can view metrics across all organizations.

---

## Key Metrics

### Adoption Metrics

| Metric | Description |
|--------|-------------|
| **Total seats** | Number of Copilot licenses assigned |
| **Active users** | Users who used Copilot in the last 30 days |
| **Adoption rate** | Active users / Total seats × 100% |
| **New users this month** | First-time users in the current month |

### Usage Metrics

| Metric | Description |
|--------|-------------|
| **Suggestions shown** | Total inline suggestions displayed |
| **Suggestions accepted** | Suggestions the user accepted (Tab) |
| **Acceptance rate** | Accepted / Shown × 100% |
| **Lines of code accepted** | Total lines of AI-generated code accepted |
| **Chat messages** | Number of Copilot Chat interactions |
| **Agent mode sessions** | Number of agent mode activations |

### Language Breakdown

See which programming languages are used most with Copilot:

| Language | Acceptance Rate | Usage Share |
|----------|----------------|-------------|
| TypeScript | 35% | 28% |
| Python | 38% | 24% |
| JavaScript | 33% | 18% |
| Java | 30% | 12% |
| Go | 32% | 8% |
| Others | 28% | 10% |

*(Example data — actual rates vary by organization)*

---

## Copilot Metrics API

For programmatic access to metrics, use the GitHub REST API:

```bash
# Get Copilot usage metrics for your organization
curl -H "Authorization: Bearer YOUR_TOKEN" \
  https://api.github.com/orgs/YOUR_ORG/copilot/usage
```

Response includes:
- Daily breakdown of suggestions and acceptances
- Per-language statistics
- Active user counts
- Feature-specific usage (chat, completions, agent mode)

---

## Measuring ROI

### Quantitative Indicators

| Indicator | How to Measure |
|-----------|---------------|
| Code velocity | Compare PRs/week before and after Copilot |
| Time to first commit | How quickly developers start contributing |
| Test coverage | Has test coverage improved? |
| Bug rate | Has the bug rate changed? |
| Acceptance rate | Higher rates suggest useful suggestions |

### Qualitative Indicators

- Developer satisfaction surveys
- Onboarding feedback (new hires using Copilot)
- Time saved on repetitive tasks (self-reported)
- Reduced context switching

---

## Best Practices for Metrics

1. **Baseline first** — Measure productivity before enabling Copilot
2. **Allow ramp-up time** — 30-60 days for developers to learn Copilot
3. **Do not use acceptance rate alone** — A low rate does not mean low value; developers may learn from dismissed suggestions
4. **Combine with surveys** — Quantitative + qualitative gives the full picture
5. **Track monthly trends** — Look for improvement over time, not snapshot values

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 11: Security & Admin](README.md) |
| Previous Lesson | [IP Indemnity](ip-indemnity.md) |
| Next Module | [Module 12: Real-World Projects](../12-real-world-projects/) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
