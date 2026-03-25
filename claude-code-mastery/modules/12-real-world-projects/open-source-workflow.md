# Open Source Contribution Workflow

**Module 12, Lesson 4 — Claude Code Mastery**

**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Overview

Contributing to open source requires understanding unfamiliar codebases quickly, following project conventions, and producing quality pull requests. Claude Code excels at all of these. This lesson covers the complete workflow from forking a repository to responding to review feedback.

---

## Step 1: Forking and Cloning

```bash
# Fork and clone via GitHub CLI
gh repo fork owner/project-name --clone
cd project-name

# Start Claude Code
claude
```

Orient yourself immediately:

```
What is the tech stack of this project? List the main frameworks, languages,
and build tools based on the config files.
```

---

## Step 2: Understanding the Codebase

Build a mental model before changing anything:

```
Explain the architecture of this project. What are the main directories,
how does data flow, and what are the key entry points?
```

Drill into the area you plan to change:

```
How does the authentication system work? Trace the flow from login to
session creation and show the key files.
```

| Exploration Prompt | When to Use |
|-------------------|-------------|
| "Explain the architecture..." | First time in any codebase |
| "How does X feature work?" | Before modifying a feature |
| "What are the coding conventions?" | Before writing new code |
| "What CI checks must my PR pass?" | Before submitting |

---

## Step 3: Finding Issues to Work On

```
Read CONTRIBUTING.md and summarize the contribution guidelines.
What labels should I look for on issues?
```

Use the GitHub CLI to find suitable issues:

```bash
gh issue list --label "good first issue" --state open
gh issue view 42
```

Assess the issue with Claude Code:

```
I want to work on issue #42: "Add rate limiting to /api/search."
Look at the current implementation and tell me what changes are needed.
Are there existing rate limiting patterns in this codebase?
```

---

## Step 4: Making the Contribution

```bash
git checkout -b fix/rate-limit-search-endpoint
```

Implement with Claude Code:

```
Implement rate limiting for /api/search based on issue #42. Follow existing
patterns in this codebase. Use the same libraries and coding style the
project already uses.
```

Self-review before submitting:

```
Review the changes. Check they follow CONTRIBUTING.md, include tests,
and do not break anything. Update docs if the project requires it.
```

---

## Step 5: Creating a Quality PR

Study the project's PR conventions:

```
Look at the last 5 merged PRs using gh. What format do they use for
titles and descriptions? Draft a PR title and body for my changes.
```

Create the PR:

```bash
git push -u origin fix/rate-limit-search-endpoint
gh pr create --title "Add rate limiting to /api/search" --body "## Summary
Implements rate limiting for /api/search (#42).
## Changes
- Rate limit middleware (100 req/15 min per IP)
- Tests for enforcement and 429 responses
Closes #42"
```

---

## Step 6: Responding to Review Feedback

Address reviewer comments by pasting their feedback into Claude Code:

```
The reviewer said: "Use a sliding window instead of fixed window, and make
the limit configurable." Update the implementation accordingly.
```

If you disagree, ask Claude Code to help articulate your reasoning:

```
The reviewer suggests Redis for state. This project has no Redis. Help me
write a polite response explaining why in-memory limiting suffices here.
```

---

## Contribution Checklist

| Step | Action |
|------|--------|
| Read CONTRIBUTING.md | Understand guidelines before coding |
| Check existing patterns | Match the project's style, not yours |
| Run tests locally | Never submit a PR with failing tests |
| Update documentation | If the project expects it for new features |
| Write a clear PR description | Reference the issue, explain what and why |
| Respond to reviews promptly | Address feedback within a few days |

---

## Common Pitfalls

| Pitfall | How to Avoid |
|---------|-------------|
| Ignoring conventions | Ask Claude to check CONTRIBUTING.md first |
| Over-engineering | Match the complexity of existing code |
| No tests | Ask Claude to identify required coverage |
| Unfocused PRs | Keep changes scoped to one issue |
| Skipping local CI | Run `claude -p "Run the CI checks"` before pushing |

---

## Navigation

| Direction | Link |
|-----------|------|
| Previous Lesson | [CI/CD Automation](cicd-automation.md) |
| Module Overview | [README](README.md) |
| Course Home | [Claude Code Mastery](../../) |

---

> **Contribution Tip:** The best open source contributors spend more time reading than writing. Use Claude Code to understand unfamiliar code before changing anything.
