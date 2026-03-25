# Team Setup & Onboarding

**Module 09, Lesson 1 — Claude Code Mastery**

**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Overview

Getting one developer productive with Claude Code is straightforward. Getting an entire team aligned requires shared configurations, conventions, and onboarding processes. This lesson covers the layered configuration system that lets teams commit shared settings to version control while preserving individual developer preferences.

---

## Configuration Layers

Claude Code uses a layered configuration system. Settings merge from broadest to most specific:

| Layer | File | Committed to Git? | Scope |
|-------|------|--------------------|-------|
| Enterprise | `/etc/claude-code/CLAUDE.md` | N/A (managed) | All users on machine |
| Project instructions | `CLAUDE.md` (repo root) | Yes | All team members |
| Project settings | `.claude/settings.json` | Yes | Shared tool permissions |
| Personal settings | `.claude/settings.local.json` | No (gitignored) | Individual preferences |
| User instructions | `~/.claude/CLAUDE.md` | No | All projects for one user |

---

## Shared CLAUDE.md (Project Level)

The most important file for team alignment is `CLAUDE.md` at your repository root. Commit it to git so every team member gets the same instructions. A well-structured team CLAUDE.md should include project architecture, coding standards, testing requirements, forbidden patterns, and PR conventions.

```json
// .claude/settings.json — shared project settings
{
  "permissions": {
    "allow": [
      "Bash(npm run test)",
      "Bash(npm run lint)",
      "Bash(npm run build)"
    ],
    "deny": [
      "Bash(rm -rf *)",
      "Bash(git push --force)"
    ]
  }
}
```

This file should be committed to git. It ensures every team member has the same tool permissions without needing to approve common commands individually.

---

## Personal Settings (Gitignored)

Individual developers can override or extend shared settings with `.claude/settings.local.json`:

```json
{
  "permissions": {
    "allow": [
      "Bash(docker compose up)",
      "Bash(kubectl get pods)"
    ]
  },
  "preferences": {
    "thinkingEffort": "high"
  }
}
```

This file should be listed in `.gitignore`. It lets developers add personal tool permissions or preferences without affecting the team configuration.

---

## Team Conventions and Coding Standards

| Convention Area | What to Specify | Example |
|----------------|-----------------|---------|
| Language style | Formatting, linting rules | "Use Prettier defaults, ESLint with airbnb config" |
| Naming | Variables, files, components | "camelCase for functions, PascalCase for components" |
| Architecture | Patterns, directory structure | "Follow hexagonal architecture in src/domain/" |
| Testing | Framework, coverage, location | "Jest tests in __tests__/, min 80% coverage" |
| Git workflow | Branch names, commit format | "feat/TICKET-123-description, conventional commits" |

---

## Onboarding New Team Members

Create a structured onboarding experience by combining Claude Code with your project setup:

1. **Clone the repo** — CLAUDE.md and `.claude/settings.json` come along automatically
2. **Run setup** — have Claude assist: `claude "set up this project for local development"`
3. **Verify tooling** — shared permissions mean no manual approval for standard commands
4. **Create personal settings** — copy a template for `.claude/settings.local.json`

```json
// .claude/settings.local.json.template (committed to git)
{
  "permissions": { "allow": [] },
  "preferences": { "thinkingEffort": "medium" }
}
```

---

## Custom Slash Commands for Team Workflows

Teams can create shared slash commands by adding Markdown files to `.claude/commands/`:

| Command | File | Purpose |
|---------|------|---------|
| `/project:review` | `.claude/commands/review.md` | Run team-standard code review |
| `/project:deploy-check` | `.claude/commands/deploy-check.md` | Pre-deployment validation |
| `/project:onboard` | `.claude/commands/onboard.md` | Guide new developer through setup |
| `/project:migrate` | `.claude/commands/migrate.md` | Database migration workflow |

These files live in the repo and are available to every team member automatically.

---

## Best Practices Summary

| Practice | Reason |
|----------|--------|
| Commit `CLAUDE.md` to repo root | Ensures all team members get the same project context |
| Commit `.claude/settings.json` | Shares tool permissions across the team |
| Gitignore `.claude/settings.local.json` | Preserves individual developer preferences |
| Create slash command templates | Standardizes common workflows |
| Document architecture in CLAUDE.md | Reduces onboarding time and improves code consistency |
| Review CLAUDE.md in PRs | Treat AI instructions as code — they deserve review |

---

## Navigation

| Direction | Link |
|-----------|------|
| Previous | [Module 09 Overview](README.md) |
| Next | [Enterprise Configuration](enterprise-config.md) |
| Module Home | [Module 09: Team & Enterprise](README.md) |
