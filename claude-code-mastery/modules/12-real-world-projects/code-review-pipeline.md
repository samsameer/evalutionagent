# Automated Code Review Pipeline

**Module 12, Lesson 2 — Claude Code Mastery**

**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Overview

Code review is where bugs get caught, standards get enforced, and knowledge gets shared. This lesson shows how to use Claude Code for both manual reviews and fully automated review pipelines that run on every pull request. You will set up custom review rules, configure review hooks, and integrate everything into GitHub Actions.

---

## Manual Reviews with /review

The simplest way to review code is the built-in `/review` command. Open Claude Code in your repository and run:

```
/review
```

Claude Code analyzes the current diff and provides feedback on:
- Logic errors and potential bugs
- Security vulnerabilities
- Performance concerns
- Style inconsistencies
- Missing error handling

You can also review specific files or a range of commits:

```
Review the changes in src/api/ from the last 3 commits. Focus on error
handling and input validation.
```

---

## Customizing Reviews with REVIEW.md

Create a `REVIEW.md` file at your repository root to define custom review criteria. Claude Code reads this file when performing reviews.

```markdown
# Code Review Standards

## Always Check
- All API endpoints validate input with Zod schemas
- Database queries use parameterized values (no string concatenation)
- Error responses never leak stack traces or internal details
- New functions have JSDoc comments with parameter descriptions
- Async functions have try/catch blocks or .catch() handlers

## Security Rules
- No secrets or API keys in source code
- Authentication middleware applied to all protected routes
- SQL injection prevention verified on any raw queries
- CORS configuration reviewed for any new endpoints

## Performance Rules
- No N+1 query patterns — use Prisma includes for relations
- Large lists must support pagination
- Images and static assets use Next.js Image component

## Test Requirements
- New utility functions require unit tests
- New API routes require integration tests
- Bug fixes require a regression test
```

When Claude Code runs a review, it checks your code against these specific criteria rather than applying generic advice.

---

## Enterprise Code Review Service

For organizations using the Claude Code Enterprise plan, you can set up a centralized review service that runs across all repositories:

1. **Configure the review policy** in your organization settings:

```json
{
  "review": {
    "enabled": true,
    "auto_review_prs": true,
    "required_before_merge": false,
    "model": "claude-sonnet-4-20250514",
    "max_files_per_review": 50
  }
}
```

2. **Deploy the review bot** by installing the Claude Code GitHub App on your organization and enabling review mode for selected repositories.

3. **Set organization-wide review rules** that apply across all repos while allowing per-repo REVIEW.md overrides.

---

## Custom Review Hook

Hooks let you run custom logic before or after Claude Code performs actions. Here is a review hook that enforces additional checks:

```json
// .claude/settings.json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Review",
        "hooks": [
          {
            "type": "command",
            "command": "node scripts/post-review-check.js"
          }
        ]
      }
    ]
  }
}
```

The post-review script can enforce gates:

```javascript
// scripts/post-review-check.js
const { execSync } = require('child_process');

// Ensure tests pass after review suggestions are applied
try {
  execSync('npm test --silent', { stdio: 'pipe' });
  console.log('All tests pass after review changes.');
} catch (error) {
  console.error('Tests failed after applying review suggestions.');
  console.error('Fix failing tests before committing.');
  process.exit(1);
}
```

---

## GitHub Actions: Automated Review on PR

This workflow runs Claude Code review automatically on every pull request:

```yaml
# .github/workflows/claude-review.yml
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
      - name: Checkout code
        uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - name: Install Claude Code
        run: npm install -g @anthropic-ai/claude-code

      - name: Run review
        env:
          ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
        run: |
          claude -p "Review the changes in this pull request. Check against
          REVIEW.md standards if present. Output your review as structured
          markdown with sections: Summary, Issues Found, Suggestions,
          and Approval Recommendation." \
          --output-format json > review-output.json

      - name: Post review comment
        uses: actions/github-script@v7
        with:
          script: |
            const fs = require('fs');
            const output = JSON.parse(fs.readFileSync('review-output.json', 'utf8'));
            await github.rest.pulls.createReview({
              owner: context.repo.owner,
              repo: context.repo.repo,
              pull_number: context.payload.pull_request.number,
              body: output.result,
              event: 'COMMENT'
            });
```

---

## Review Pipeline Best Practices

| Practice | Rationale |
|----------|-----------|
| Keep REVIEW.md under 50 rules | Too many rules dilute focus and increase cost |
| Use specific, testable criteria | "Validate input" is vague; "All POST endpoints use Zod schemas" is actionable |
| Set `required_before_merge: false` initially | Let the team build trust in automated reviews before gating merges |
| Review the reviewer | Periodically check Claude Code's review output for false positives |
| Combine with linters | Use ESLint for formatting rules, Claude Code for logic and architecture review |

---

## Combining Manual and Automated Reviews

The most effective pipeline uses both approaches:

1. **Automated review** runs on every PR via GitHub Actions, catching common issues instantly
2. **Developer runs `/review`** locally before pushing to fix issues early
3. **Human reviewer** focuses on architecture and design decisions, not style or basic bugs
4. **REVIEW.md evolves** as the team adds new rules based on recurring issues

This layered approach reduces review turnaround time while maintaining high code quality standards.

---

## Navigation

| Direction | Link |
|-----------|------|
| Previous Lesson | [Build a Full-Stack App](fullstack-app.md) |
| Next Lesson | [CI/CD Automation](cicd-automation.md) |
| Module Overview | [Module 12: Real-World Projects](README.md) |

---

> **Review Tip:** Start with a small REVIEW.md containing your team's top 5 most common review comments. Expand it over time as you identify patterns in the feedback Claude Code gives.
