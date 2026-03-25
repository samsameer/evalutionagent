# Workflow Templates

**Claude Code Mastery — March 2026**
**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Workflow 1: Feature Development

```
Step 1 — Plan:      "Read the codebase. Propose an implementation plan for [feature] with file changes."
Step 2 — Implement: "Implement the plan. Follow CLAUDE.md conventions."
Step 3 — Test:      "Write unit tests covering happy path, edge cases, errors. Run and fix failures."
Step 4 — Review:    "Review all changes for bugs, security issues, missing error handling."
Step 5 — Commit:    "Create a commit with a conventional commit message."
```

## Workflow 2: Bug Fixing

```
Step 1 — Reproduce:  "Read bug report: [paste]. Find relevant code and explain the cause."
Step 2 — Root Cause: "Trace execution path. Identify the specific lines responsible."
Step 3 — Fix:        "Fix with minimal change. No side effects."
Step 4 — Verify:     "Write a regression test. Run all related tests."
Step 5 — Document:   "Add a code comment if the fix is non-obvious."
```

## Workflow 3: Code Review Assistant

```
Interactive:
> "Review `git diff main...HEAD`. Check for: logic errors, security issues,
>  performance concerns, style violations, missing tests. Give actionable feedback."

Headless (CI/CD):
$ claude -p "Review PR changes. Output markdown with severity labels." --max-turns 5
```

## Workflow 4: Refactoring

```
Step 1 — Assess:  "Analyze [file]. Identify code smells, duplication, improvements by priority."
Step 2 — Plan:    "Create a refactoring plan in small safe steps. Tests must pass after each."
Step 3 — Execute: "Perform step 1: [specific refactor]. Run tests." (repeat per step)
Step 4 — Validate:"Run full test suite. Confirm no breaking API changes."
```

## Workflow 5: Test Generation

```
Step 1 — Analyze: "List all public functions in [file]. Identify needed test cases."
Step 2 — Generate:"Write tests following existing project patterns and framework."
Step 3 — Run:     "Run tests. Fix failures. Ensure no flaky tests."
Step 4 — Coverage:"Run coverage report. Add tests for uncovered branches."
```

## Workflow 6: Documentation Generation

```
Step 1 — Inventory:   "List all public APIs and modules needing documentation."
Step 2 — Docstrings:  "Write JSDoc/docstrings for undocumented public functions."
Step 3 — README:      "Update README with current setup, API overview, examples."
Step 4 — API Reference:"Generate endpoint reference with request/response examples."
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
