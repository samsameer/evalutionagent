# Built-in Tools Reference

**Module 05, Lesson 2 — Claude Code Mastery**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Claude Code has **11 built-in tools** that it uses to interact with your filesystem, shell, and the web. Each tool is optimized for a specific job. This lesson is a complete reference for every tool, its parameters, and when to use it.

---

## Tool Quick Reference

| Tool | Purpose | Key Strength |
|------|---------|--------------|
| Read | Read files, images, PDFs, notebooks | Multimodal — handles any file type |
| Edit | Precise string replacement in files | Surgical edits without rewriting |
| Write | Create new files or full rewrites | Complete file creation |
| Bash | Execute shell commands | Full system access |
| Glob | Find files by name pattern | Fast pattern matching at any scale |
| Grep | Search file contents with regex | Ripgrep-powered content search |
| WebFetch | Fetch content from a URL | Read documentation and web pages |
| WebSearch | Search the web | Find solutions and references online |
| Agent | Spawn sub-agents for parallel work | Concurrent multi-task execution |
| TodoWrite | Track multi-step task progress | Maintain a checklist of sub-tasks |
| NotebookEdit | Edit Jupyter notebook cells | Modify `.ipynb` files in place |

---

## Read

Reads a file from the local filesystem. Supports text files, images (PNG, JPG), PDFs, and Jupyter notebooks (`.ipynb`).

**Parameters:**

| Parameter | Required | Description |
|-----------|----------|-------------|
| `file_path` | Yes | Absolute path to the file |
| `offset` | No | Line number to start reading from |
| `limit` | No | Number of lines to read |
| `pages` | No | Page range for PDFs (e.g., `"1-5"`) |

**Key behaviors:**
- Returns content with line numbers (cat -n format)
- For large PDFs (10+ pages), you **must** specify the `pages` parameter
- Maximum 20 PDF pages per request
- Images are presented visually (Claude is multimodal)
- Reads up to 2000 lines by default

**Example prompt:**

```
Read the file at /src/utils/auth.ts and tell me what it does.
```

```
Read pages 3-7 of the PDF at /docs/spec.pdf.
```

---

## Edit

Performs exact string replacements in files. This is the primary tool for modifying existing code.

**Parameters:**

| Parameter | Required | Description |
|-----------|----------|-------------|
| `file_path` | Yes | Absolute path to the file |
| `old_string` | Yes | The exact text to find and replace |
| `new_string` | Yes | The replacement text |
| `replace_all` | No | Replace all occurrences (default: false) |

**Key behaviors:**
- The file **must** be read first before editing
- `old_string` must be unique in the file, or the edit fails
- Preserves exact indentation from the original file
- Use `replace_all: true` for renaming variables across a file

**Example prompt:**

```
In /src/app.ts, change the port from 3000 to 8080.
```

---

## Write

Creates a new file or completely rewrites an existing file.

**Parameters:**

| Parameter | Required | Description |
|-----------|----------|-------------|
| `file_path` | Yes | Absolute path to the file |
| `content` | Yes | The full content to write |

**Key behaviors:**
- Overwrites existing files entirely
- For existing files, Read must be called first
- Prefer Edit for modifications — Write sends the entire file content
- Never creates documentation files unless explicitly requested

**Example prompt:**

```
Create a new file at /src/utils/logger.ts with a Winston logger setup.
```

---

## Bash

Executes shell commands and returns their output.

**Parameters:**

| Parameter | Required | Description |
|-----------|----------|-------------|
| `command` | Yes | The shell command to execute |
| `timeout` | No | Timeout in milliseconds (max 600,000 / 10 min) |
| `run_in_background` | No | Run asynchronously, get notified on completion |

**Key behaviors:**
- Default timeout is 120,000 ms (2 minutes)
- Working directory persists between calls, but shell state does not
- Use `run_in_background` for long-running tasks (builds, tests)
- Avoid using Bash for tasks that have dedicated tools (e.g., use Grep instead of `rg`)

**Example prompt:**

```
Run the test suite with npm test and show me the results.
```

```
Start the dev server in the background so I can keep working.
```

---

## Glob

Finds files by name pattern. Works efficiently on codebases of any size.

**Parameters:**

| Parameter | Required | Description |
|-----------|----------|-------------|
| `pattern` | Yes | Glob pattern (e.g., `"**/*.ts"`) |
| `path` | No | Directory to search in (defaults to cwd) |

**Common patterns:**

| Pattern | Matches |
|---------|---------|
| `"**/*.ts"` | All TypeScript files recursively |
| `"src/**/*.test.js"` | All test files under `src/` |
| `"*.json"` | JSON files in the current directory only |
| `"**/README.md"` | All README files at any depth |

**Example prompt:**

```
Find all Python files in the project.
```

---

## Grep

Searches file contents using regular expressions, powered by ripgrep.

**Parameters:**

| Parameter | Required | Description |
|-----------|----------|-------------|
| `pattern` | Yes | Regex pattern to search for |
| `path` | No | File or directory to search in |
| `glob` | No | Filter by file glob (e.g., `"*.ts"`) |
| `type` | No | File type filter (e.g., `"py"`, `"js"`) |
| `output_mode` | No | `"files_with_matches"` (default), `"content"`, or `"count"` |
| `-A` | No | Lines to show after each match |
| `-B` | No | Lines to show before each match |
| `-C` / `context` | No | Lines to show before and after each match |
| `-i` | No | Case-insensitive search |
| `-n` | No | Show line numbers (default: true) |
| `multiline` | No | Enable multiline matching |
| `head_limit` | No | Limit output to first N entries |

**Example prompt:**

```
Search for all usages of "useAuth" across the React components.
```

---

## WebFetch

Fetches content from a URL and returns it for analysis.

**Use cases:**
- Reading API documentation pages
- Fetching remote configuration files
- Pulling changelogs or release notes
- Reading GitHub issues or discussions

**Example prompt:**

```
Fetch the Express.js routing documentation and summarize the middleware pattern.
```

---

## WebSearch

Searches the web and returns results.

**Use cases:**
- Finding solutions to error messages
- Looking up library APIs or best practices
- Checking for known issues or CVEs
- Researching unfamiliar concepts

**Example prompt:**

```
Search the web for "TypeScript 5.4 satisfies operator examples".
```

---

## Agent

Spawns a sub-agent that can work independently, using the same set of tools. Multiple agents can run in parallel.

**Use cases:**
- Investigating multiple files simultaneously
- Running parallel searches across different parts of a codebase
- Breaking complex tasks into concurrent sub-tasks

**Example prompt:**

```
Look at both the frontend auth flow and the backend auth middleware at the same time
and tell me if they are consistent.
```

---

## TodoWrite

Tracks progress on multi-step tasks by maintaining a checklist.

**Use cases:**
- Large refactoring operations with many files
- Multi-step migration tasks
- Tracking which items in a list have been processed

Claude uses this internally to keep track of progress on complex requests. You rarely need to invoke it directly.

---

## NotebookEdit

Edits cells in Jupyter notebooks (`.ipynb` files).

**Use cases:**
- Adding, removing, or modifying notebook cells
- Updating code cells with fixes
- Adding markdown documentation cells

**Example prompt:**

```
In the notebook at /analysis/explore.ipynb, fix the pandas import in cell 3.
```

---

## Choosing the Right Tool

| Task | Best Tool | Avoid |
|------|-----------|-------|
| Read a file | Read | `cat` via Bash |
| Find files by name | Glob | `find` via Bash |
| Search file contents | Grep | `grep` or `rg` via Bash |
| Modify existing code | Edit | Write (sends full file) |
| Create a new file | Write | `echo >` via Bash |
| Run tests or builds | Bash | — |
| Look something up online | WebSearch | — |
| Read a web page | WebFetch | `curl` via Bash |

---

[← Module Overview](README.md) | [Git Integration →](git-integration.md)

---

*Module 05, Lesson 2 — Claude Code Mastery — March 2026*
