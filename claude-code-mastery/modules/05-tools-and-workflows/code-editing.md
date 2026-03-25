# Code Editing Workflows

**Module 05, Lesson 4 — Claude Code Mastery**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Editing code is the most frequent operation Claude Code performs. Understanding how the Edit and Write tools work — and when to use each — is essential for getting clean, predictable results. This lesson covers the mechanics of file editing, multi-file workflows, and real-world refactoring patterns.

---

## How the Edit Tool Works

The Edit tool performs **exact string replacement**. You give it an `old_string` and a `new_string`, and it swaps one for the other.

```
Edit(
  file_path: "/src/config.ts",
  old_string: "const PORT = 3000;",
  new_string: "const PORT = process.env.PORT || 8080;"
)
```

### Rules and Constraints

| Rule | Detail |
|------|--------|
| **Read before edit** | The file must be read first, or the edit fails |
| **Unique match** | `old_string` must appear exactly once in the file |
| **Exact whitespace** | Indentation must match the file exactly |
| **replace_all** | Set to `true` to replace every occurrence (useful for renames) |

### When Edits Fail

If the `old_string` is not unique, the edit fails. Claude handles this by:

1. Expanding the `old_string` to include more surrounding context
2. Re-attempting with a longer, unique match

**Example of a non-unique string:**

```typescript
// This appears multiple times — edit will fail
return null;
```

**Fix — include surrounding context:**

```typescript
// This is unique — edit will succeed
  if (!user) {
    return null;
  }
```

---

## When to Use Edit vs. Write

| Scenario | Tool | Reason |
|----------|------|--------|
| Change a function signature | Edit | Surgical, minimal change |
| Add a new import line | Edit | Inserts into existing code |
| Rename a variable across a file | Edit (`replace_all`) | Replaces every occurrence |
| Create a brand-new file | Write | File does not exist yet |
| Completely rewrite a file | Write | Replacing all content |
| Small fix (1-5 lines) | Edit | Efficient and precise |
| Large restructuring (80%+ changed) | Write | Easier than many small edits |

**General rule:** If you are changing less than half the file, use Edit. If you are rewriting most of it, use Write.

---

## Multi-File Editing Workflows

Claude frequently edits multiple files in a single task. The typical pattern:

### Step 1: Discover Files

```
Grep("handleAuth", type: "ts")
→ src/auth/handler.ts
→ src/middleware/auth.ts
→ src/routes/login.ts
```

### Step 2: Read Each File

Claude reads all relevant files to understand the full context before making changes.

### Step 3: Plan the Changes

Claude determines the minimal set of edits needed across all files.

### Step 4: Apply Edits

Edits are applied file by file, with each change verified.

### Step 5: Verify

Claude runs tests or linters to confirm the changes work.

**Example prompt for multi-file editing:**

```
Rename the `getUserToken` function to `getSessionToken` everywhere it appears.
```

Claude will:
1. **Grep** for `getUserToken` to find all files
2. **Read** each file
3. **Edit** each file with `replace_all: true`
4. **Grep** again to confirm no occurrences remain

---

## Refactoring Across Codebases

For large-scale refactoring, Claude combines tools in a systematic workflow:

### Extract a Function

```
Extract the validation logic from handleSubmit in /src/forms/contact.ts
into a separate validateContactForm function.
```

Claude will:
1. Read the file to understand the current code
2. Edit to add the new function definition
3. Edit to replace the inline logic with a function call
4. Check for any other files that might need the extracted function

### Move Code Between Files

```
Move the DateUtils class from /src/utils/helpers.ts into its own file
at /src/utils/date-utils.ts and update all imports.
```

Claude will:
1. Read the source file
2. Write the new file with the extracted class
3. Edit the source file to remove the class
4. Grep for all imports of the class
5. Edit each importing file to update the import path

### Change an Interface

```
Add an optional `metadata` field to the User interface and handle it
in all places that create or consume User objects.
```

Claude will:
1. Read the interface definition
2. Edit to add the new field
3. Grep for all usages of the User type
4. Read and edit each file to handle the new field appropriately

---

## Example Workflow: Add a Feature

**Prompt:** "Add a rate limiter middleware to the Express app."

| Step | Tool | Action |
|------|------|--------|
| 1 | Glob | Find existing middleware files for convention reference |
| 2 | Read | Read the app setup file and an existing middleware |
| 3 | Write | Create `/src/middleware/rate-limiter.ts` |
| 4 | Edit | Add import and `app.use()` call in `/src/app.ts` |
| 5 | Write | Create `/src/middleware/rate-limiter.test.ts` |
| 6 | Bash | Run `npm test` to verify |

---

## Example Workflow: Fix a Bug

**Prompt:** "Users report a 500 error when uploading files larger than 10MB."

| Step | Tool | Action |
|------|------|--------|
| 1 | Grep | Search for file upload handling code |
| 2 | Read | Read the upload handler and config |
| 3 | Grep | Search for size limit or max size settings |
| 4 | Edit | Fix the size limit or add proper error handling |
| 5 | Bash | Run relevant tests |
| 6 | Bash | Create a commit with the fix |

---

## Example Workflow: Refactor

**Prompt:** "Convert all callback-based database functions to async/await."

| Step | Tool | Action |
|------|------|--------|
| 1 | Grep | Find all callback patterns (e.g., `function.*callback`) |
| 2 | Read | Read each file to understand the callback structure |
| 3 | Edit | Convert each function to async/await, file by file |
| 4 | Grep | Verify no callback patterns remain |
| 5 | Bash | Run the full test suite |
| 6 | Bash | Commit with a descriptive message |

---

## Tips for Better Edits

1. **Be specific in prompts** — "Change the port to 8080" is better than "Update the config"
2. **Let Claude read first** — Claude produces better edits when it has full context
3. **Ask for verification** — "Fix the bug and run the tests" ensures Claude checks its own work
4. **Use replace_all for renames** — Avoids missing occurrences
5. **Prefer small edits** — Multiple precise edits are safer than one large rewrite

---

[← Git Integration](git-integration.md) | [Web Search & Fetch →](web-search-fetch.md)

---

*Module 05, Lesson 4 — Claude Code Mastery — March 2026*
