# Workflow Templates

**Claude Code Mastery — March 2026**
**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Workflow 1: Feature Development

Step-by-step workflow for building a new feature from start to finish.

```
Step 1 — Plan
> "Read the codebase and explain how [existing feature] works.
>  Then propose an implementation plan for [new feature] with file changes listed."

Step 2 — Implement
> "Implement the plan from above. Create the necessary files and modify
>  existing ones. Follow the conventions in CLAUDE.md."

Step 3 — Test
> "Write unit tests for the new feature. Cover happy path, edge cases,
>  and error scenarios. Run the tests and fix any failures."

Step 4 — Review
> "Review all changes you made. Check for bugs, security issues,
>  missing error handling, and adherence to project conventions."

Step 5 — Commit
> "Create a well-structured commit with a conventional commit message.
>  Group related changes logically."
```

## Workflow 2: Bug Fixing

Systematic approach to diagnosing and fixing bugs.

```
Step 1 — Reproduce
> "Read the bug report: [paste bug]. Find the relevant code and explain
>  what is causing this behavior."

Step 2 — Root Cause
> "Trace the execution path and identify the root cause. Show me the
>  specific lines of code responsible."

Step 3 — Fix
> "Fix the bug. Make the minimal change necessary to resolve the issue
>  without side effects."

Step 4 — Verify
> "Write a regression test that would have caught this bug.
>  Run all related tests to confirm nothing is broken."

Step 5 — Document
> "Add a code comment explaining why this fix was needed if the logic
>  is non-obvious. Update the changelog if we have one."
```

## Workflow 3: Code Review Assistant

Use Claude Code to review pull requests or code changes.

```
Single command approach:
> "Review the diff from `git diff main...HEAD`. Check for:
>  1. Logic errors and potential bugs
>  2. Security vulnerabilities
>  3. Performance concerns
>  4. Code style and convention violations
>  5. Missing tests or error handling
>  Provide feedback as actionable comments with file and line references."

CI/CD headless approach:
$ claude -p "Review the changes in this PR. Output a markdown summary
  with severity labels (critical/warning/suggestion) for each finding." \
  --max-turns 5 --allowedTools bash,read
```

## Workflow 4: Refactoring

Safe, incremental refactoring with test validation.

```
Step 1 — Assess
> "Analyze [file/module]. Identify code smells, duplication,
>  and opportunities for improvement. List them by priority."

Step 2 — Plan
> "Create a refactoring plan that can be done in small, safe steps.
>  Each step should keep tests passing."

Step 3 — Execute incrementally
> "Perform refactoring step 1: [specific refactor].
>  Run tests after to confirm nothing breaks."
> (repeat for each step)

Step 4 — Validate
> "Run the full test suite. Compare the public API before and after
>  to confirm no breaking changes."
```

## Workflow 5: Test Generation

Generate comprehensive tests for existing code.

```
Step 1 — Analyze coverage
> "Read [file] and list all public functions/methods.
>  For each, identify what test cases are needed:
>  happy path, edge cases, error cases, boundary values."

Step 2 — Generate tests
> "Write tests for [file] following the test patterns already
>  used in this project. Use the same test framework and assertions."

Step 3 — Run and fix
> "Run the new tests. Fix any failures. Ensure all tests pass
>  and there are no flaky tests."

Step 4 — Coverage check
> "Run coverage report: [coverage command].
>  Identify any remaining uncovered branches and add tests for them."
```

## Workflow 6: Documentation Generation

Create or update project documentation.

```
Step 1 — Inventory
> "List all public APIs, exported functions, and key modules
>  in this project that need documentation."

Step 2 — Generate docs
> "Write JSDoc/docstring comments for all undocumented public
>  functions in [file/directory]. Include parameter descriptions,
>  return types, and usage examples."

Step 3 — README
> "Update the README.md with current setup instructions,
>  API overview, and usage examples based on the actual code."

Step 4 — API docs
> "Generate an API reference document covering all endpoints
>  with request/response examples."
```

## Workflow 7: Database Migration

Safely create and apply database schema changes.

```
Step 1 — Plan:    "Analyze current schema. Show what migration is needed for [change]. Consider data preservation."
Step 2 — Create:  "Create a migration with both up and down. Include index changes."
Step 3 — Validate:"Review for data loss risks, FK constraints, and backward compatibility."
Step 4 — Update:  "Update application models/types to match the new schema."
Step 5 — Test:    "Run migration against test database. Verify the app works with new schema."
```

## Workflow 8: Legacy Code Migration

Migrate code from one framework/language to another.

```
Step 1 — Inventory: "Analyze [source dir]. List files, responsibilities, dependencies, complexity."
Step 2 — Map:       "Map each source file to its [new framework] equivalent."
Step 3 — Migrate:   "Migrate [file] to [target]. Preserve logic. Use proper [target] conventions."
Step 4 — Test:      "Write integration tests comparing old and new implementations."
Step 5 — Cleanup:   "Remove deprecated code, update imports, verify integration."
```

---

> **Tip:** Save your most-used workflow prompts in your CLAUDE.md under a `## Common Workflows` section so Claude can reference them automatically.
