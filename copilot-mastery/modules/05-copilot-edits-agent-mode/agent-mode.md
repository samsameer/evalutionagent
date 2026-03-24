# Agent Mode — Autonomous Coding

**Module 05, Lesson 2 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Agent Mode is the **most transformative feature** of GitHub Copilot. When you activate agent mode, Copilot becomes an autonomous coding agent that can plan implementations, create and edit files, run terminal commands, read output, fix errors, and iterate until the task is complete — all from a single natural language instruction.

---

## What Makes Agent Mode Different

| Capability | Regular Chat | Copilot Edits | Agent Mode |
|-----------|-------------|---------------|------------|
| Answer questions | Yes | No | Yes |
| Edit files | Suggest only | With review | Autonomously |
| Create new files | No | Yes | Yes |
| Run terminal commands | No | No | **Yes** |
| Read command output | No | No | **Yes** |
| Fix errors automatically | No | No | **Yes** |
| Install packages | No | No | **Yes** |
| Use MCP tools | No | No | **Yes** |
| Multi-step planning | No | Limited | **Yes** |
| Self-correction loop | No | No | **Yes** |

---

## How to Activate Agent Mode

### Method 1: Chat Panel

1. Open Copilot Chat (`Ctrl+Alt+I` / `Cmd+Option+I`)
2. Click the **mode selector** at the top of the chat panel
3. Select **"Agent"**
4. Type your task description
5. Press Enter

### Method 2: Keyboard Shortcut

- Use `Ctrl+Alt+I` to open chat, then switch to Agent mode

### Settings Required

Ensure these settings are enabled in VS Code:

```json
{
  "chat.agent.enabled": true,
  "github.copilot.chat.agent.runTasks": true
}
```

---

## The Agentic Loop in Detail

When you give agent mode a task, it follows this loop:

```
┌──────────────────────────────────────────────┐
│           Agent Mode Execution Flow           │
└──────────────────────────────────────────────┘

Step 1: UNDERSTAND
  │  Read your prompt and analyze the request
  │  Examine workspace structure and relevant files
  │
Step 2: PLAN
  │  Break the task into steps
  │  Identify files to create, modify, or delete
  │  Determine terminal commands needed
  │
Step 3: EXECUTE
  │  Create/edit files with proposed changes
  │  Run terminal commands (npm install, build, test)
  │  Read output from commands
  │
Step 4: VALIDATE
  │  Check command output for errors
  │  If errors found → go back to Step 3 (fix and retry)
  │  If no errors → continue to next step or finish
  │
Step 5: ITERATE
  │  Repeat Steps 3-4 for each part of the plan
  │  Self-correct as needed
  │
Step 6: COMPLETE
     Present results for your review
     Show all changes made
```

---

## Real-World Example: Building a REST API

### Your Prompt:
```
Create a REST API for a todo application using Express.js and TypeScript.
Include:
- CRUD endpoints (GET, POST, PUT, DELETE)
- Input validation with Zod
- Error handling middleware
- Unit tests with Jest
- A package.json with all dependencies
```

### What Agent Mode Does:

**Step 1:** Examines your project structure

**Step 2:** Plans the implementation:
- Create `package.json` with dependencies
- Create `tsconfig.json`
- Create `src/index.ts` (app entry point)
- Create `src/routes/todos.ts` (CRUD routes)
- Create `src/middleware/error-handler.ts`
- Create `src/schemas/todo.schema.ts` (Zod validation)
- Create `src/__tests__/todos.test.ts` (Jest tests)

**Step 3:** Creates all files, then runs:
```bash
npm install
```

**Step 4:** Reads the output — if packages installed successfully, continues. If not, fixes `package.json` and retries.

**Step 5:** Runs the build:
```bash
npx tsc
```

If TypeScript compilation fails, agent mode reads the errors and fixes the code.

**Step 6:** Runs tests:
```bash
npm test
```

If tests fail, it reads the failure output and fixes the test or the implementation.

**Step 7:** Presents the final result — all files created, all commands passed.

---

## Terminal Command Approval

By default, agent mode asks for your **approval before running terminal commands**. You will see a prompt like:

```
Copilot wants to run the following command:
  npm install express @types/express zod jest ts-jest

[Allow] [Deny] [Always Allow]
```

| Option | Description |
|--------|-------------|
| **Allow** | Run this specific command |
| **Deny** | Block this command |
| **Always Allow** | Allow this type of command without future prompts |

### Auto-Approve Settings

For trusted projects, you can configure auto-approval:

```json
{
  "github.copilot.chat.agent.autoApprove": [
    "npm install",
    "npm test",
    "npm run build",
    "npx tsc"
  ]
}
```

> **Security Note:** Be careful with auto-approve. Always review what commands agent mode wants to run, especially in unfamiliar projects.

---

## What Agent Mode Can Run

| Command Type | Examples | Typically Safe |
|-------------|---------|---------------|
| Package install | `npm install`, `pip install`, `cargo add` | Yes |
| Build | `npm run build`, `go build`, `cargo build` | Yes |
| Test | `npm test`, `pytest`, `go test` | Yes |
| Lint | `eslint .`, `ruff check` | Yes |
| Type check | `npx tsc --noEmit`, `mypy` | Yes |
| Format | `prettier --write .`, `black .` | Yes |
| Database | `prisma migrate dev`, `alembic upgrade` | Caution |
| Deploy | `vercel deploy`, `fly deploy` | Review carefully |

---

## Tips for Effective Agent Mode Usage

### 1. Write Clear, Detailed Prompts

```
BAD:  "Make a website"
GOOD: "Create a Next.js 14 application with a landing page that has a hero section,
       features grid, and contact form. Use Tailwind CSS for styling. Include
       proper TypeScript types and responsive design."
```

### 2. Start Small, Then Expand

Begin with a focused task, verify the result, then ask for additions. This is better than a massive prompt that may go in the wrong direction.

### 3. Provide Architecture Context

```
"Use the repository pattern. Services should be in src/services/,
 routes in src/routes/, and types in src/types/. Follow the existing
 patterns in the codebase."
```

### 4. Let It Self-Correct

When agent mode encounters an error, **let it try to fix it** before intervening. The self-correction loop is one of its strongest capabilities.

### 5. Review All Changes

After agent mode completes, carefully review:
- All created/modified files
- Terminal command history
- Test results
- Any security implications

---

## Limitations of Agent Mode

- Cannot access external services without MCP tools
- May not understand complex business logic without clear instructions
- Can sometimes get stuck in correction loops — if this happens, provide guidance
- Resource-intensive — uses more premium requests than standard chat
- Currently only available in VS Code (not JetBrains or other editors)

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 05: Edits & Agent Mode](README.md) |
| Previous Lesson | [Copilot Edits](copilot-edits.md) |
| Next Lesson | [MCP Tools in Agent Mode](mcp-tools.md) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
