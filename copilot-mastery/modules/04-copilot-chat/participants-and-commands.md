# Chat Participants & Slash Commands

**Module 04, Lesson 2 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Chat participants and slash commands are **power features** that dramatically expand what Copilot Chat can do. Participants give Copilot access to specific domains (your workspace, terminal, VS Code itself), while slash commands provide shortcuts for common actions.

---

## Chat Participants

Chat participants are invoked with the `@` symbol. Each participant gives Copilot specialized access to a different domain.

### @workspace — Your Entire Codebase

The most powerful participant. `@workspace` gives Copilot access to your **entire project structure** — all files, imports, dependencies, and patterns.

**Use cases:**
```
@workspace How is the database connection configured?
@workspace What API endpoints are defined in this project?
@workspace Find all usages of the UserService class
@workspace What testing framework does this project use?
@workspace Explain the architecture of this application
```

**How it works:**
1. Copilot indexes your workspace files
2. It uses embeddings to find relevant files for your question
3. It reads the most relevant files and provides a contextualized answer
4. File paths are linked — you can click to navigate

### @terminal — Terminal Context

`@terminal` gives Copilot access to your integrated terminal, including recent commands, output, and errors.

**Use cases:**
```
@terminal Why did my last command fail?
@terminal How do I fix this npm error?
@terminal What does this build output mean?
@terminal Suggest a command to find large files in this directory
```

### @vscode — VS Code Itself

`@vscode` helps you with VS Code settings, extensions, keybindings, and features.

**Use cases:**
```
@vscode How do I change the color theme?
@vscode What extension should I use for Python formatting?
@vscode How do I set up a debug configuration for Node.js?
@vscode Show me the keyboard shortcut for multi-cursor editing
```

### @github — GitHub Integration

`@github` connects Copilot to your GitHub repositories, issues, PRs, and organization.

**Use cases:**
```
@github What are the open issues in this repository?
@github Show me the recent pull requests
@github What CI checks are required for merging?
@github Who is the code owner for the /src/auth directory?
```

> **Note:** `@github` requires the GitHub Pull Requests extension and appropriate authentication.

---

## Slash Commands

Slash commands are shortcuts that tell Copilot Chat what kind of action you want. They can be used alone or combined with participants.

### Complete Slash Command Reference

| Command | Description | Example |
|---------|-------------|---------|
| `/explain` | Explain selected code or concept | `/explain What does this regex do?` |
| `/fix` | Fix bugs or errors in selected code | `/fix This function throws a null pointer exception` |
| `/tests` | Generate unit tests for selected code | `/tests Generate tests for the UserService class` |
| `/doc` | Generate documentation/comments | `/doc Add JSDoc comments to this function` |
| `/new` | Scaffold a new project or file | `/new Create a React component for a login form` |
| `/newNotebook` | Create a new Jupyter notebook | `/newNotebook Data analysis for sales CSV` |
| `/optimize` | Improve performance of selected code | `/optimize This database query is slow` |
| `/clear` | Clear the chat conversation history | `/clear` |
| `/help` | Show available commands and features | `/help` |

### Using Slash Commands with Participants

You can combine participants and slash commands for precision:

```
@workspace /explain How does the authentication middleware work?
@workspace /tests Generate integration tests for the API routes
@workspace /fix The search feature returns duplicate results
@terminal /explain What does the error in my last command mean?
@vscode /doc How do I create a custom snippet?
```

---

## Slash Commands in Detail

### /explain — Understand Code

Select code in your editor, then:

```
/explain

# Or be specific:
/explain What is the time complexity of this algorithm?
/explain Why does this use a WeakMap instead of a regular Map?
/explain Walk me through this code step by step
```

Copilot provides a detailed explanation with:
- Line-by-line breakdown
- Purpose and intent
- Edge cases and potential issues
- Related concepts

### /fix — Debug and Fix Issues

```
/fix This function doesn't handle empty arrays
/fix The API returns 500 when the user is not authenticated
/fix TypeScript error: Property 'name' does not exist on type 'unknown'
```

Copilot:
1. Analyzes the issue
2. Identifies the root cause
3. Proposes a fix with a diff
4. Explains why the fix works

### /tests — Generate Tests

```
/tests
/tests Generate tests using Jest and React Testing Library
/tests Cover edge cases including null input and empty strings
/tests Write integration tests for the payment processing flow
```

Copilot generates:
- Test file structure
- Test cases for happy paths
- Edge case tests
- Mock setups if needed
- Proper assertions

### /doc — Generate Documentation

```
/doc
/doc Add comprehensive JSDoc with @param, @returns, and @example
/doc Generate a README for this module
/doc Add inline comments explaining the business logic
```

### /new — Scaffold New Code

```
/new Create an Express.js REST API with CRUD operations for a blog
/new Build a React component for a data table with sorting and pagination
/new Create a Python FastAPI application with SQLAlchemy ORM
/new Scaffold a GitHub Actions workflow for CI/CD
```

### /optimize — Improve Performance

```
/optimize This SQL query takes 5 seconds on a table with 1M rows
/optimize The React component re-renders too frequently
/optimize This loop has O(n²) complexity — can it be improved?
```

---

## Tips for Effective Chat Interactions

1. **Be specific** — "Fix the bug" is vague. "Fix the null pointer exception in getUserById when the user doesn't exist" is actionable.

2. **Provide context** — Select relevant code before chatting, or use `#file` references.

3. **Use the right participant** — `@workspace` for codebase questions, `@terminal` for command issues.

4. **Chain commands** — Ask follow-up questions to refine the response.

5. **Use slash commands** — They prime Copilot for the right type of response.

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 04: Copilot Chat](README.md) |
| Previous Lesson | [Chat Modes](chat-modes.md) |
| Next Lesson | [Context Variables & References](context-variables.md) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
