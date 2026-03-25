# Automated Code Review Pipeline

**Module 12, Lesson 2 — Claude Code Mastery**

**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Overview

Code review is one of the highest-leverage activities in development, and Claude Code can automate large parts of it. This lesson covers manual reviews with `/review`, custom review rules via `REVIEW.md`, pre-commit review hooks, and GitHub Actions that review every pull request automatically.

---

## Manual Reviews with /review

The `/review` command analyzes your changes and provides feedback on quality, bugs, and style:

```bash
# Review all uncommitted changes
claude -p "/review"

# Review a specific file
claude -p "Review src/api/tasks.ts for security issues and error handling"

# Review a branch diff
git diff main..feature-branch | claude -p "Review this diff for bugs and style issues"
```

> **Tip:** Pipe a focused diff rather than the entire codebase. Smaller scope produces more actionable feedback.

---

## REVIEW.md Customization

Create a `REVIEW.md` in your project root to define standards Claude Code follows during reviews:

```markdown
# Code Review Standards

## Always Check
- API routes must validate input with Zod schemas
- Database queries must use parameterized inputs
- Error responses must not expose stack traces

## Style
- Use early returns to reduce nesting
- Maximum function length: 40 lines
- Prefer named exports over default exports

## Security
- No secrets or API keys in source code
- All user input must be sanitized before database insertion
- Auth middleware must protect all non-public routes

## Testing
- New routes require at least one happy-path and one error-path test
```

When this file exists, Claude Code incorporates these rules into every review for the project.

---

## Enterprise Code Review Service

Teams on enterprise plans can configure centralized review at the organization level:

| Feature | Description |
|---------|-------------|
| **Org-wide rules** | Standards applied across all repositories |
| **Custom rule sets** | Different profiles for frontend, backend, and infrastructure |
| **Severity blocking** | Block merges only on critical findings |

```json
{
  "review": {
    "enabled": true,
    "ruleSets": ["security", "performance", "style"],
    "blockOnSeverity": "high"
  }
}
```

---

## Custom Review Hook

Run a review automatically before every commit using hooks in `.claude/settings.json`:

```json
{
  "hooks": {
    "PreCommit": [
      {
        "matcher": "",
        "hook": {
          "type": "command",
          "command": "claude -p 'Review staged changes. If you find critical bugs or security issues, respond BLOCK and explain. Otherwise respond PASS.' --output-format json | node scripts/check-review.js"
        }
      }
    ]
  }
}
```

The companion `scripts/check-review.js`:

```javascript
const fs = require("fs");
const input = fs.readFileSync("/dev/stdin", "utf8");
const result = JSON.parse(input);
const text = result.result || "";

if (text.includes("BLOCK")) {
  console.error("Review blocked the commit:");
  console.error(text);
  process.exit(1);
}
console.log("Review passed.");
```

---

## GitHub Actions: Review on Every PR

Create `.github/workflows/code-review.yml`:

```yaml
name: Claude Code Review

on:
  pull_request:
    types: [opened, synchronize]

permissions:
  contents: read
  pull-requests: write

jobs:
  review:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - name: Install Claude Code
        run: npm install -g @anthropic-ai/claude-code

      - name: Run review
        env:
          ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
        run: |
          git diff origin/main...HEAD > /tmp/pr-diff.txt
          claude -p "Review this diff against our REVIEW.md standards. Format as a markdown checklist with pass/fail for each rule." < /tmp/pr-diff.txt > /tmp/review.md

      - name: Post review comment
        uses: actions/github-script@v7
        with:
          script: |
            const fs = require('fs');
            const body = fs.readFileSync('/tmp/review.md', 'utf8');
            await github.rest.issues.createComment({
              owner: context.repo.owner,
              repo: context.repo.repo,
              issue_number: context.issue.number,
              body: `## Automated Code Review\n\n${body}`
            });
```

---

## Best Practices

| Practice | Details |
|----------|---------|
| **Keep REVIEW.md updated** | Treat it as a living document |
| **Scope reviews tightly** | Review the diff, not the whole codebase |
| **Use severity levels** | Block merges only on critical issues |
| **Combine with linters** | Claude reviews complement ESLint, not replace it |
| **Audit Claude's output** | Periodically check for false positives |

---

## Navigation

| Direction | Link |
|-----------|------|
| Previous Lesson | [Build a Full-Stack App](fullstack-app.md) |
| Next Lesson | [CI/CD Automation](cicd-automation.md) |
| Module Overview | [README](README.md) |

---

> **Pipeline Tip:** Start with the GitHub Actions workflow and add the pre-commit hook once your team trusts the automated output. Gradual adoption reduces friction.
