# CI/CD Automation

**Module 12, Lesson 3 — Claude Code Mastery**

**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Overview

Claude Code's headless mode and SDK make it a powerful component in CI/CD pipelines. This lesson covers GitHub Actions workflows, headless automation, pre-commit hooks, automated testing, and security scanning.

---

## Headless Mode for Automation

Run Claude Code non-interactively in pipeline environments:

```bash
# Basic headless execution
claude -p "Run the test suite and summarize any failures"

# JSON output for programmatic parsing
claude -p "List all TODO comments in the codebase" --output-format json

# Limit turns to prevent runaway sessions
claude -p "Fix the failing test in src/api/tasks.test.ts" --max-turns 10

# Pre-authorize tools
claude -p "Refactor utils.ts to use async/await" --allowedTools "Edit,Read,Bash"
```

| Flag | Purpose |
|------|---------|
| `-p` | Print mode, non-interactive output to stdout |
| `--output-format json` | Structured output for scripting |
| `--max-turns 10` | Prevents infinite loops and cost spikes |
| `--allowedTools` | Skips interactive permission prompts |

---

## GitHub Actions: Test and Fix Pipeline

```yaml
name: Test and Auto-Fix
on:
  push:
    branches: [main, "feature/**"]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with: { node-version: 20 }
      - run: npm ci
      - name: Run tests
        id: tests
        run: npm test 2>&1 | tee /tmp/test-output.txt
        continue-on-error: true
      - name: Auto-fix with Claude Code
        if: steps.tests.outcome == 'failure'
        env:
          ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
        run: |
          npm install -g @anthropic-ai/claude-code
          claude -p "Tests failed: $(cat /tmp/test-output.txt)
          Fix the source code, not the tests." --max-turns 15
      - name: Re-run tests
        if: steps.tests.outcome == 'failure'
        run: npm test
```

> **Caution:** Auto-fix workflows should run on feature branches only, never on main.

---

## Pre-Commit Hooks with Claude Code

Install Husky (`npm install -D husky && npx husky init`) and create `.husky/pre-commit`:

```bash
#!/bin/sh
npx lint-staged
STAGED=$(git diff --cached --name-only --diff-filter=ACM | grep -E '\.(ts|tsx)$')
if [ -n "$STAGED" ]; then
  git diff --cached | claude -p "Review for critical bugs and security issues
  only. Respond PASS or FAIL with explanation." > /tmp/claude-review.txt
  grep -q "FAIL" /tmp/claude-review.txt && { cat /tmp/claude-review.txt; exit 1; }
fi
```

---

## Automated Testing Pipeline

Generate tests for new files that lack coverage:

```yaml
name: Test Coverage Gate
on:
  pull_request:
    types: [opened, synchronize]
jobs:
  coverage:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with: { fetch-depth: 0 }
      - uses: actions/setup-node@v4
        with: { node-version: 20 }
      - run: npm ci
      - name: Generate missing tests
        env:
          ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
        run: |
          npm install -g @anthropic-ai/claude-code
          for file in $(git diff --name-only origin/main...HEAD | grep '\.ts$' | grep -v '\.test\.'); do
            TEST="${file%.ts}.test.ts"
            [ ! -f "$TEST" ] && claude -p "Write Vitest tests for $file. Save to $TEST." --max-turns 10
          done
      - run: npm run test:coverage
```

---

## Security Scanning

```yaml
name: Security Scan
on:
  pull_request:
    types: [opened, synchronize]
jobs:
  security:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm audit --json > /tmp/audit.json
        continue-on-error: true
      - name: Claude security analysis
        env:
          ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
        run: |
          npm install -g @anthropic-ai/claude-code
          claude -p "Security review: 1) hardcoded secrets 2) auth logic
          3) injection/XSS 4) npm audit: $(cat /tmp/audit.json | head -100)
          Provide a severity-rated markdown report." > /tmp/security-report.md
      - uses: actions/upload-artifact@v4
        with:
          name: security-report
          path: /tmp/security-report.md
```

---

## Pipeline Design Principles

| Principle | Rationale |
|-----------|-----------|
| **Fast checks first** | Run linters before Claude Code to fail fast |
| **Scope tightly** | Send diffs, not the entire repo |
| **Set turn limits** | Always use `--max-turns` to control cost |
| **Branch protection** | Never let auto-fixes push to main |
| **Cache the CLI** | Cache the npm package across runs |
| **Manage secrets** | Store API keys in GitHub Secrets only |

---

## Navigation

| Direction | Link |
|-----------|------|
| Previous Lesson | [Automated Code Review Pipeline](code-review-pipeline.md) |
| Next Lesson | [Open Source Contribution Workflow](open-source-workflow.md) |
| Module Overview | [README](README.md) |

---

> **Cost Tip:** Set a spending limit on the API key used in CI. A misconfigured pipeline without turn limits can consume significant credits.
