# AI-Powered Pull Request Summaries

**Module 07, Lesson 2 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Writing clear PR descriptions is essential for code review, but it takes time. Copilot can **automatically generate comprehensive PR summaries** that describe what changed, why it changed, and what reviewers should focus on.

---

## Generating a PR Summary

### When Creating a New PR

1. Go to your repository on GitHub.com
2. Click **"New pull request"** or navigate to the PR creation page
3. In the PR description field, look for the **Copilot icon** (sparkle/star)
4. Click it to generate an AI-powered summary
5. Copilot analyzes all commits and file changes in the PR
6. A summary is generated and inserted into the description field
7. Review and edit the summary as needed

### What Copilot Generates

A typical Copilot PR summary includes:

```markdown
## Summary

This PR implements JWT-based authentication for the REST API.

### Changes Made

- **New file: `src/middleware/auth.ts`** — JWT verification middleware
  that validates tokens and attaches user context to requests
- **Modified: `src/routes/index.ts`** — Applied auth middleware to
  all protected routes
- **Modified: `src/types/express.d.ts`** — Extended Express Request
  type with user property
- **New file: `src/__tests__/auth.test.ts`** — Unit tests for
  authentication middleware

### Key Decisions

- Used `jsonwebtoken` library for JWT handling
- Public routes (`/login`, `/register`) are excluded from auth
- Token expiry set to 24 hours

### Testing

- Added 12 unit tests covering valid tokens, expired tokens,
  missing tokens, and malformed tokens
- All tests passing
```

---

## Customizing Generated Summaries

The generated summary is a **starting point** — you should always review and customize it:

- **Add business context** — Why was this change needed?
- **Link to issues** — Add `Closes #123` references
- **Add screenshots** — For UI changes
- **Note deployment considerations** — Database migrations, config changes
- **Highlight risks** — Breaking changes, performance implications

---

## Using Copilot Summary in PR Templates

You can combine Copilot summaries with your team's PR template:

```markdown
## Description
<!-- Copilot generates this section -->

## Related Issues
<!-- You fill this in manually -->
Closes #456

## Testing Done
<!-- Copilot can help, but verify -->

## Screenshots
<!-- Add manually for UI changes -->

## Deployment Notes
<!-- Add manually -->
```

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 07: GitHub.com](README.md) |
| Previous Lesson | [Copilot Chat on GitHub.com](copilot-chat-web.md) |
| Next Lesson | [Copilot Code Review](code-review.md) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
