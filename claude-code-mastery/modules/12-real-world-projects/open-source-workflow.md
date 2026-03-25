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

Go deeper into the area you plan to change:

```
How does the authentication system work? Trace the flow from login request
to session creation and show the key files involved.
```

```
What testing framework does this project use? Show the test directory
structure and the conventions for naming tests.
```

| Prompt | When to Use |
|--------|-------------|
| "Explain the architecture..." | First time in any codebase |
| "How does X feature work?" | Before modifying a feature |
| "What are the coding conventions?" | Before writing new code |
| "Show me the test patterns" | Before writing tests |
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
Review the changes you just made. Check they follow CONTRIBUTING.md
conventions, include tests, and do not introduce breaking changes.
```

Check for documentation requirements:

```
Does this project require doc updates for new features? If so, update
the relevant docs to mention the rate limiting behavior.
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

gh pr create --title "Add rate limiting to /api/search endpoint" --body "$(cat <<'EOF'
## Summary
Implements rate limiting for /api/search as described in #42.

## Changes
- Added rate limit middleware using existing express-rate-limit package
- Configured 100 requests per 15-minute window per IP
- Added tests for rate limit enforcement and 429 responses
- Updated API docs with rate limit details

## Testing
- Unit tests for rate limit middleware
- Integration test verifying 429 after exceeding limit
- All existing tests pass

Closes #42
EOF
)"
```

---

## Step 6: Responding to Review Feedback

Address reviewer comments efficiently:

```
The reviewer said: "Use a sliding window algorithm instead of fixed window,
and make the limit configurable via environment variables."
Update the implementation to address both points. Keep existing tests passing.
```

After updating:

```bash
git add -A && git commit -m "Address review: sliding window + configurable limit"
git push
```

If you disagree with feedback, use Claude Code to articulate your reasoning:

```
The reviewer suggests using Redis for rate limit state. This project has no
Redis dependency. Help me write a polite response explaining why in-memory
rate limiting is sufficient here, with supporting references.
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
