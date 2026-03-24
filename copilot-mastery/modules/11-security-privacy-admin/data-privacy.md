# Data Privacy & Code Handling

**Module 11, Lesson 1 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

One of the most common concerns about AI coding assistants is: **"What happens to my code?"** This lesson provides a clear, detailed answer for every Copilot plan.

---

## What Data Is Sent to GitHub?

When you use Copilot, the following data is transmitted to GitHub's servers:

| Data Type | What It Includes |
|-----------|-----------------|
| **Prompt data** | Code from your current file, open tabs, and surrounding context |
| **User engagement data** | Whether you accepted, modified, or dismissed a suggestion |
| **Metadata** | Language, IDE, extension version, anonymized telemetry |
| **Chat messages** | Your questions and the AI's responses (for Copilot Chat) |

---

## Data Retention by Plan

| Plan | Code Used for Training? | Prompt Retention | Suggestion Retention |
|------|------------------------|------------------|---------------------|
| **Free** | No (opt-out default since 2024) | Transient — not stored | Not stored |
| **Pro** | No (opt-out default) | Transient — not stored | Not stored |
| **Pro+** | No | Transient — not stored | Not stored |
| **Business** | **Never** | **Not retained** | **Not retained** |
| **Enterprise** | **Never** | **Not retained** | **Not retained** |

### Key Points

- **No plan uses your code to train AI models** (as of 2024, this is the default for all plans)
- **Business and Enterprise** have the strongest guarantees — code is never retained beyond the immediate request-response cycle
- **Prompts and suggestions** are processed in real-time and discarded
- All data is **encrypted in transit** (TLS 1.2+) and **encrypted at rest** where applicable

---

## Data Flow Diagram

```
┌──────────────┐     Encrypted      ┌──────────────┐
│  Your Editor │────(TLS 1.2+)────►│  GitHub       │
│  (VS Code,   │                    │  Copilot      │
│   JetBrains) │◄───────────────────│  Service      │
└──────────────┘     Suggestion     └──────┬───────┘
                                           │
                                    ┌──────▼───────┐
                                    │  AI Model     │
                                    │  (GPT-4o,     │
                                    │   Claude,     │
                                    │   Gemini)     │
                                    └──────────────┘

What is NOT stored:
  ✗ Your source code
  ✗ Your prompts (after processing)
  ✗ Generated suggestions (after delivery)

What IS stored:
  ✓ Anonymized usage telemetry (opt-out available)
  ✓ Feedback data (thumbs up/down if you provide it)
```

---

## Telemetry and Opt-Out

### VS Code Telemetry Settings

You can control telemetry in VS Code settings:

```json
{
  // Disable all VS Code telemetry
  "telemetry.telemetryLevel": "off",

  // Or limit to errors only
  "telemetry.telemetryLevel": "error"
}
```

### GitHub Copilot Telemetry

In your GitHub account settings:
1. Go to [github.com/settings/copilot](https://github.com/settings/copilot)
2. Find the **"Allow GitHub to use my code snippets for product improvements"** toggle
3. Set to **Off** (this is the default)

---

## Compliance and Certifications

GitHub Copilot (Business and Enterprise) is covered under:

| Certification | Description |
|--------------|-------------|
| SOC 2 Type II | Security, availability, and confidentiality controls |
| ISO 27001 | Information security management |
| GDPR | European data protection compliance |
| CCPA | California consumer privacy compliance |
| FedRAMP | US government cloud security (GitHub Enterprise Cloud) |

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 11: Security & Admin](README.md) |
| Next Lesson | [Content Exclusions](content-exclusions.md) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
