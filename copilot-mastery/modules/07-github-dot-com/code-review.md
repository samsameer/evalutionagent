# Copilot Code Review

**Module 07, Lesson 3 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Copilot can act as an **AI code reviewer** on your pull requests. It analyzes the diff, identifies potential issues, suggests improvements, and can even generate review comments — helping you catch bugs before they reach production.

---

## How to Request a Copilot Code Review

### Automatic Review

For organizations with Copilot Enterprise or Business, Copilot can be configured to **automatically review all PRs**:

1. Go to **Repository Settings** → **Code review** (or Organization settings)
2. Enable **"Copilot code review"**
3. Configure which types of issues Copilot should flag

### Manual Review Request

On any PR page:

1. Click the **"Reviewers"** section in the PR sidebar
2. Select **"Copilot"** as a reviewer
3. Copilot analyzes the PR and posts review comments

---

## What Copilot Reviews

| Category | What It Checks |
|----------|---------------|
| **Bugs** | Null pointer risks, off-by-one errors, race conditions |
| **Security** | SQL injection, XSS, hardcoded secrets, insecure patterns |
| **Performance** | Unnecessary loops, memory leaks, N+1 queries |
| **Code Quality** | Code duplication, naming conventions, complexity |
| **Best Practices** | Error handling, logging, input validation |
| **Documentation** | Missing comments for complex logic |

---

## Types of Review Comments

### Suggestion Comments

Copilot provides concrete code suggestions that you can apply with one click:

```
suggestion
  Copilot suggests: Consider using optional chaining here to prevent
  potential null reference errors.

- const name = user.profile.name;
+ const name = user?.profile?.name;
```

### Warning Comments

```
Copilot: ⚠️ This SQL query concatenates user input directly,
which could be vulnerable to SQL injection. Consider using
parameterized queries instead.
```

### Informational Comments

```
Copilot: ℹ️ This function has a cyclomatic complexity of 12.
Consider breaking it into smaller, focused functions for
better testability and readability.
```

---

## Responding to Copilot Reviews

- **Accept suggestions** — Click "Apply suggestion" to commit the fix directly
- **Dismiss** — If the suggestion is not relevant, dismiss it
- **Discuss** — Reply to Copilot's comment to get more context or alternative solutions
- **Batch apply** — Apply multiple suggestions in a single commit

---

## Configuring Review Sensitivity

For Enterprise organizations, you can configure what Copilot focuses on:

| Setting | Description |
|---------|-------------|
| Security focus | Prioritize security vulnerabilities |
| Performance focus | Focus on performance issues |
| Style enforcement | Enforce coding style and conventions |
| Bug detection | Focus on potential bugs and logic errors |
| Custom rules | Define organization-specific review rules |

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 07: GitHub.com](README.md) |
| Previous Lesson | [PR Summaries](pr-summaries.md) |
| Next Lesson | [Copilot Workspace](copilot-workspace.md) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
