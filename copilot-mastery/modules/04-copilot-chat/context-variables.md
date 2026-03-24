# Context Variables & References

**Module 04, Lesson 3 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Context variables let you **precisely control** what information Copilot Chat has access to when generating responses. Instead of hoping Copilot picks up the right context, you can explicitly reference files, selections, terminal output, and more.

---

## All Context Variables

| Variable | Syntax | Description |
|----------|--------|-------------|
| **#file** | `#file:path/to/file.ts` | Reference a specific file in your workspace |
| **#selection** | `#selection` | The currently selected text in the editor |
| **#editor** | `#editor` | The entire visible content of the active editor |
| **#codebase** | `#codebase` | Search across your entire codebase (similar to @workspace) |
| **#terminalLastCommand** | `#terminalLastCommand` | The last command and its output from the terminal |
| **#terminalSelection** | `#terminalSelection` | Selected text in the terminal |
| **#problems** | `#problems` | Current errors and warnings from the Problems panel |
| **#changes** | `#changes` | Current uncommitted Git changes |
| **#gitDiff** | `#gitDiff` | The git diff of staged or unstaged changes |

---

## Using #file — Reference Specific Files

The `#file` variable is one of the most useful context tools. It tells Copilot to look at a specific file when answering your question.

### How to Use

Type `#file:` and VS Code will show an autocomplete list of files in your workspace:

```
How does #file:src/auth/auth.service.ts handle token refresh?

Compare the approach in #file:src/api/v1/routes.ts with #file:src/api/v2/routes.ts

Write tests for #file:src/utils/validation.ts using the patterns from #file:src/utils/__tests__/helpers.test.ts
```

### Drag and Drop

You can also **drag a file** from the Explorer panel into the chat input. This automatically inserts the `#file:` reference.

### Multiple File References

You can reference multiple files in a single message:

```
Refactor #file:src/services/user.service.ts and #file:src/services/order.service.ts to use a shared base class
```

---

## Using #selection — Current Selection

`#selection` refers to whatever text you have selected in the active editor.

```
# First, select some code in your editor, then:
/explain #selection
/fix #selection — this function doesn't handle the edge case where items is empty
/tests Generate tests for #selection
```

This is equivalent to selecting code and using inline chat (`Ctrl+I`), but gives you the flexibility of the full chat panel.

---

## Using #editor — Active Editor Content

`#editor` gives Copilot the full visible content of your currently active editor tab.

```
#editor What patterns do you see in this file?
#editor Suggest improvements for code quality
#editor Are there any potential security vulnerabilities?
```

---

## Using #codebase — Workspace-Wide Search

`#codebase` tells Copilot to search across your entire workspace for relevant information.

```
#codebase Where is the database connection string configured?
#codebase What services depend on the UserRepository?
#codebase Show me all API endpoints that require authentication
```

> **Difference from @workspace:** `#codebase` is a context variable that adds codebase context to your message, while `@workspace` is a participant that routes your entire question through workspace-aware processing. In practice, they are very similar.

---

## Using #terminalLastCommand — Terminal Output

`#terminalLastCommand` captures the most recent command and its output from the VS Code integrated terminal.

```
# Run a command in the terminal that fails:
$ npm run build

# Then in Copilot Chat:
#terminalLastCommand Why did this build fail? How do I fix it?
```

This is incredibly useful for:
- Debugging build errors
- Understanding test failures
- Fixing deployment issues
- Interpreting compiler errors

---

## Using #problems — IDE Diagnostics

`#problems` gives Copilot access to the current errors and warnings shown in VS Code's Problems panel.

```
#problems Fix all the TypeScript errors in my project
#problems Explain what these ESLint warnings mean
#problems Which of these problems are critical and which can be ignored?
```

---

## Using #changes and #gitDiff — Git Context

```
#changes Summarize what I've changed in this session
#changes Write a commit message for my current changes
#gitDiff Review my staged changes for any issues
#gitDiff Are there any potential bugs in my diff?
```

---

## Combining Context Variables

The real power comes from combining multiple context variables:

```
Using the patterns in #file:src/services/base.service.ts, refactor #selection to follow the same pattern

#terminalLastCommand This test failed. Look at #file:src/__tests__/auth.test.ts and fix the issue

Review #changes and compare against #file:.eslintrc.json to ensure my changes follow the linting rules
```

---

## Tips for Using Context Variables

1. **Be explicit** — Use `#file:` references instead of hoping Copilot finds the right file
2. **Select before chatting** — Use `#selection` to give Copilot focused context
3. **Leverage terminal output** — `#terminalLastCommand` is perfect for debugging
4. **Combine variables** — Multiple references give Copilot richer context
5. **Use autocomplete** — After typing `#file:`, wait for the autocomplete to find your file

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 04: Copilot Chat](README.md) |
| Previous Lesson | [Chat Participants & Slash Commands](participants-and-commands.md) |
| Next Lesson | [Vision & Image Understanding](vision-capabilities.md) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
