# CI/CD Pipeline Setup

**Module 12, Lesson 3 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

In this project, you will use Copilot to set up a complete CI/CD pipeline using GitHub Actions — from basic testing to deployment.

---

## Step 1: Basic CI Pipeline

Ask Copilot Chat:

```
Create a GitHub Actions workflow for CI that:
1. Triggers on push to main and pull requests
2. Sets up Node.js 20
3. Installs dependencies with npm ci
4. Runs linting (ESLint)
5. Runs type checking (tsc --noEmit)
6. Runs tests with coverage
7. Uploads coverage report as an artifact
8. Fails if coverage drops below 80%
```

### Generated Workflow: `.github/workflows/ci.yml`

```yaml
name: CI

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'

      - name: Install dependencies
        run: npm ci

      - name: Run linter
        run: npm run lint

      - name: Type check
        run: npx tsc --noEmit

      - name: Run tests with coverage
        run: npm test -- --coverage --coverageThreshold='{"global":{"branches":80,"functions":80,"lines":80}}'

      - name: Upload coverage
        uses: actions/upload-artifact@v4
        with:
          name: coverage-report
          path: coverage/
```

---

## Step 2: Add Copilot Coding Agent Setup

```
Add a copilot-setup-steps.yml file so the Copilot Coding Agent
can work on this repository:
```

### Generated: `.github/copilot-setup-steps.yml`

```yaml
steps:
  - name: Setup Node.js
    uses: actions/setup-node@v4
    with:
      node-version: '20'

  - name: Install dependencies
    run: npm ci

  - name: Build
    run: npm run build

  - name: Verify tests pass
    run: npm test
```

---

## Step 3: Add Deployment Pipeline

```
Add a deployment workflow that:
1. Only triggers when CI passes on main
2. Builds the application
3. Deploys to Vercel (or your preferred platform)
4. Posts the deployment URL as a PR comment
```

---

## Step 4: Add PR Automation

```
Create a workflow that automatically:
1. Assigns reviewers based on CODEOWNERS
2. Adds labels based on changed files (frontend, backend, docs)
3. Runs Copilot code review
4. Posts test results as a PR comment
```

---

## What You Built

By the end of this lesson, your repository has:

```
.github/
  workflows/
    ci.yml                    # Lint, type check, test on every PR
    deploy.yml                # Deploy on merge to main
    pr-automation.yml         # Auto-label, assign, review
  copilot-setup-steps.yml     # Enable Copilot Coding Agent
  copilot-instructions.md     # Custom instructions for Copilot
```

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 12: Real-World Projects](README.md) |
| Previous Lesson | [REST API with Tests](rest-api-tests.md) |
| Next Lesson | [Team Workflows & Best Practices](team-workflows.md) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
