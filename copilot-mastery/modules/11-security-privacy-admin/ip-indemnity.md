# IP Indemnity & Code Referencing

**Module 11, Lesson 4 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

One of the biggest concerns for businesses using AI-generated code is **intellectual property (IP) risk**. What if Copilot suggests code that is copied from a GPL-licensed project? This lesson covers GitHub's IP protections and the code referencing system.

---

## What Is IP Indemnity?

GitHub provides **IP indemnity** for Copilot Business and Enterprise customers. This means:

> If a third party sues you claiming that Copilot-generated code infringes their IP rights, **GitHub will defend you and cover any damages**, provided you used the code in accordance with GitHub's terms of service.

### Coverage Details

| Aspect | Coverage |
|--------|---------|
| **What is covered** | Copyright infringement claims from AI-generated code |
| **Who is covered** | Business and Enterprise customers |
| **Condition** | Public code filter must be enabled |
| **Not covered** | Code you wrote yourself (human-authored) |
| **Not covered** | Code from Free, Pro, or Pro+ plans |

---

## Code Referencing

Code referencing is a feature that **detects when a Copilot suggestion closely matches publicly available code** on GitHub.

### How It Works

1. Copilot generates a suggestion
2. The suggestion is compared against **a large index of public GitHub repositories**
3. If a match is found (typically >150 characters of matching code), the suggestion is flagged
4. You see the **source repository** and **license** of the matching code

### What You See

When a match is detected:

```
┌──────────────────────────────────────────────────┐
│  ⚠️ Code Reference Detected                      │
│                                                    │
│  This suggestion matches code from:               │
│  Repository: github.com/example/project            │
│  License: MIT                                      │
│  File: src/utils/helpers.ts                        │
│  Match: ~92% similarity                            │
│                                                    │
│  [Accept Anyway]  [Dismiss]  [View Source]         │
└──────────────────────────────────────────────────┘
```

### License Considerations

| License | Risk Level | Recommendation |
|---------|-----------|---------------|
| MIT | Low | Generally safe to use with attribution |
| Apache 2.0 | Low | Safe with license notice |
| BSD | Low | Safe with attribution |
| GPL v2/v3 | **High** | May require your code to be GPL — review carefully |
| AGPL | **Very High** | Copyleft extends to network use — avoid in proprietary code |
| No License | **Unknown** | Cannot determine rights — treat as restrictive |

---

## Configuring Code Referencing

### For Organizations

1. Go to **Organization Settings** → **Copilot** → **Policies**
2. Find **"Suggestions matching public code"**
3. Choose:
   - **Block** — Never show suggestions that match public code
   - **Allow** — Show all suggestions with reference info
   - **Allow for specific licenses** — Only allow matches from permissive licenses

### For Individuals

1. Go to [github.com/settings/copilot](https://github.com/settings/copilot)
2. Toggle **"Suggestions matching public code"**

---

## Recommendations

| Role | Recommended Setting |
|------|-------------------|
| Individual developer (side project) | Allow with references |
| Professional developer (commercial) | Allow with references, review matches |
| Enterprise team | Block or allow only permissive licenses |
| Open source project | Allow — your project may also be open source |

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 11: Security & Admin](README.md) |
| Previous Lesson | [Organization Policies](org-policies.md) |
| Next Lesson | [Metrics & Usage Analytics](metrics-analytics.md) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
