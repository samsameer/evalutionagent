# Copilot Workspace

**Module 07, Lesson 4 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Copilot Workspace is a **cloud-based AI development environment** on GitHub.com that lets you go from an issue or idea to a complete, tested pull request — all within your browser. It is like having an AI pair programmer that can read your codebase, plan changes, write code, and run tests.

---

## What is Copilot Workspace?

```
┌─────────────────────────────────────────────────────┐
│              Copilot Workspace Flow                   │
│                                                       │
│   Issue / Idea                                        │
│       │                                               │
│       ▼                                               │
│   ┌──────────┐                                       │
│   │  Analyze  │ ← Reads codebase, understands issue  │
│   └────┬─────┘                                       │
│        │                                              │
│        ▼                                              │
│   ┌──────────┐                                       │
│   │   Plan   │ ← Lists files to change, approach    │
│   └────┬─────┘                                       │
│        │                                              │
│        ▼                                              │
│   ┌──────────┐                                       │
│   │ Implement│ ← Writes/edits code across files     │
│   └────┬─────┘                                       │
│        │                                              │
│        ▼                                              │
│   ┌──────────┐                                       │
│   │  Validate│ ← Runs tests, checks build           │
│   └────┬─────┘                                       │
│        │                                              │
│        ▼                                              │
│   ┌──────────┐                                       │
│   │ Create PR│ ← Opens pull request with summary    │
│   └──────────┘                                       │
└─────────────────────────────────────────────────────┘
```

---

## How to Use Copilot Workspace

### Starting from an Issue

1. Open any GitHub Issue
2. Click the **"Open in Workspace"** button (or Copilot icon)
3. Copilot Workspace opens in a new browser tab
4. It analyzes the issue and your codebase
5. A **plan** is presented — listing files to change and the approach
6. Review the plan, modify if needed
7. Click **"Implement"** to generate the code
8. Review the changes in a diff view
9. Click **"Create Pull Request"** when satisfied

### Starting from Scratch

1. Navigate to your repository on GitHub.com
2. Open Copilot Workspace from the repository menu
3. Describe what you want to build or change in natural language
4. Follow the same plan → implement → review flow

---

## The Workspace Interface

| Section | Description |
|---------|-------------|
| **Task Description** | Your issue or natural language description |
| **Specification** | Copilot's understanding of what needs to be done |
| **Plan** | List of files to create/modify with descriptions |
| **Implementation** | The actual code changes shown as diffs |
| **Terminal** | Run build and test commands |
| **Pull Request** | Create a PR directly from Workspace |

---

## Editing the Plan

The plan is **fully editable**. Before Copilot implements anything, you can:

- **Add files** that Copilot missed
- **Remove files** that should not be changed
- **Modify descriptions** to guide the implementation
- **Reorder steps** for logical sequencing
- **Add constraints** like "use TypeScript strict mode" or "follow existing patterns"

---

## Example: Feature Implementation

### Issue: "Add dark mode support to the settings page"

**Copilot Workspace Plan:**

| Step | File | Action |
|------|------|--------|
| 1 | `src/contexts/ThemeContext.tsx` | Create theme context with light/dark state |
| 2 | `src/hooks/useTheme.ts` | Create hook to consume theme context |
| 3 | `src/components/Settings/ThemeToggle.tsx` | Create dark mode toggle component |
| 4 | `src/pages/Settings.tsx` | Add ThemeToggle to settings page |
| 5 | `src/styles/dark-theme.css` | Create dark mode CSS variables |
| 6 | `src/App.tsx` | Wrap app with ThemeProvider |
| 7 | `src/__tests__/ThemeToggle.test.tsx` | Add tests for toggle component |

You review this plan, perhaps add "Also update the `tailwind.config.js` for dark mode classes", then click **Implement**.

---

## Running Tests in Workspace

Copilot Workspace includes an **integrated terminal** where you can:

```bash
# Run the test suite
npm test

# Run a specific test
npm test -- --filter ThemeToggle

# Check the build
npm run build

# Start the dev server to preview
npm run dev
```

---

## Availability

| Plan | Copilot Workspace Access |
|------|------------------------|
| Free | No |
| Pro | Preview |
| Pro+ | Full access |
| Business | Preview |
| Enterprise | Full access |

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 07: GitHub.com](README.md) |
| Previous Lesson | [Code Review](code-review.md) |
| Next Module | [Module 08: Copilot Coding Agent](../08-coding-agent/) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
