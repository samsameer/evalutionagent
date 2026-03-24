# Custom Instructions

**Module 10, Lesson 1 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Custom instructions let you define **project-specific rules** that Copilot follows whenever it generates code for your repository. Instead of repeating preferences in every chat message, you write them once and Copilot applies them automatically.

---

## The `.github/copilot-instructions.md` File

Create this file at the root of your repository:

```
your-repo/
  .github/
    copilot-instructions.md    ← Your custom instructions
```

Everything in this file becomes part of Copilot's system context for your project.

---

## What to Include

### Coding Standards

```markdown
## Coding Standards

- Use TypeScript strict mode for all files
- Prefer `const` over `let`; never use `var`
- Use arrow functions for callbacks and lambdas
- Use named exports, not default exports
- Maximum line length: 100 characters
- Use 2-space indentation
```

### Architecture Patterns

```markdown
## Architecture

- Follow the repository pattern for data access
- Services go in `src/services/`
- Controllers go in `src/controllers/`
- Types and interfaces go in `src/types/`
- All database access must go through repository classes
- Use dependency injection via constructor parameters
```

### Error Handling

```markdown
## Error Handling

- Always use custom error classes from `src/errors/`
- Never catch errors silently — always log or re-throw
- Use `Result<T, E>` pattern for operations that can fail
- HTTP errors should use the `AppError` class with status codes
```

### Testing Conventions

```markdown
## Testing

- Use Jest for unit tests and Supertest for API tests
- Test files go next to source files with `.test.ts` suffix
- Use `describe` blocks to group related tests
- Mock external services, never make real API calls in tests
- Aim for 80% code coverage minimum
```

### Frameworks and Libraries

```markdown
## Tech Stack

- Frontend: React 19 with TypeScript
- Styling: Tailwind CSS v4
- State Management: Zustand
- API: tRPC with Zod validation
- Database: PostgreSQL with Prisma ORM
- Testing: Vitest + React Testing Library
```

---

## Complete Example

```markdown
# Copilot Instructions for MyApp

## Language & Style
- TypeScript strict mode, 2-space indent, semicolons required
- Prefer functional components with hooks over class components
- Use descriptive names: `fetchUserById` not `getUser`

## Architecture
- Clean architecture: controllers → services → repositories
- All API endpoints defined in `src/routes/`
- Shared types in `src/types/shared.ts`
- Use Zod for all input validation at API boundaries

## Conventions
- Dates: use `date-fns`, never `moment.js`
- HTTP client: use `fetch`, never `axios`
- Logging: use the `logger` from `src/utils/logger.ts`
- Environment variables: access via `src/config/env.ts`, never `process.env` directly

## Testing
- Jest + React Testing Library
- Every new function needs at least one test
- Use factories from `src/__tests__/factories/` for test data

## Do NOT
- Do not use `any` type — use `unknown` and narrow
- Do not use `console.log` — use the logger
- Do not commit `.env` files
- Do not use inline styles — use Tailwind classes
```

---

## How Custom Instructions Work

```
┌─────────────────────────────────────────┐
│       Your Chat/Completion Request       │
└───────────────┬─────────────────────────┘
                │
                ▼
┌─────────────────────────────────────────┐
│     .github/copilot-instructions.md      │
│     (automatically prepended)            │
└───────────────┬─────────────────────────┘
                │
                ▼
┌─────────────────────────────────────────┐
│           AI Model (LLM)                 │
│     (follows both your request AND       │
│      the custom instructions)            │
└─────────────────────────────────────────┘
```

Copilot **automatically reads** this file and includes it as context for every interaction in that repository. You do not need to reference it manually.

---

## Multiple Instruction Files

As of 2026, you can also create instruction files at different directory levels:

```
.github/copilot-instructions.md        # Project-wide
src/frontend/.copilot-instructions.md   # Frontend-specific
src/backend/.copilot-instructions.md    # Backend-specific
```

More specific instructions override broader ones when working in those directories.

---

## Tips

1. **Keep it concise** — Long instruction files dilute the most important rules
2. **Be specific** — "Use Zustand for state" is better than "Use a state management library"
3. **Include examples** — Show a code snippet of the pattern you want
4. **Update regularly** — As your project evolves, update the instructions
5. **Commit to the repo** — This file should be version-controlled so the whole team benefits

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 10: Advanced Features](README.md) |
| Next Lesson | [Model Selection & Switching](model-selection.md) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
