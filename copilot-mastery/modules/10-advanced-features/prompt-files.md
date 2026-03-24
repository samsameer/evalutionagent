# Prompt Files & Reusable Prompts

**Module 10, Lesson 3 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Prompt files (`.prompt.md`) are **reusable, shareable prompt templates** stored in your repository. They let you define common workflows that any team member can execute with a single click in Copilot Chat.

---

## What Are Prompt Files?

Prompt files are Markdown files stored in `.github/prompts/` that define structured instructions for Copilot. Think of them as **macros** or **saved commands** that you can invoke repeatedly.

```
your-repo/
  .github/
    prompts/
      new-component.prompt.md
      add-tests.prompt.md
      review-security.prompt.md
      create-api-endpoint.prompt.md
```

---

## Creating a Prompt File

### Example: `new-component.prompt.md`

```markdown
---
description: Create a new React component following project conventions
---

Create a new React component with the following requirements:

1. Use TypeScript with strict types
2. Create the component file at `src/components/{componentName}/{componentName}.tsx`
3. Create a test file at `src/components/{componentName}/{componentName}.test.tsx`
4. Create an index.ts barrel export file
5. Use functional component with React.FC type
6. Include proper prop types interface
7. Use Tailwind CSS for styling
8. Add at least 3 unit tests

Follow the existing patterns in #file:src/components/Button/Button.tsx
```

### Example: `add-tests.prompt.md`

```markdown
---
description: Add comprehensive tests for a file
---

Analyze the selected code and generate comprehensive tests:

1. Use Jest and React Testing Library
2. Cover all public functions and methods
3. Include edge cases: null inputs, empty arrays, boundary values
4. Test error scenarios and error messages
5. Use factories from #file:src/__tests__/factories/index.ts for test data
6. Follow the patterns in existing tests
7. Aim for 90%+ code coverage of the target file
```

### Example: `create-api-endpoint.prompt.md`

```markdown
---
description: Scaffold a new REST API endpoint
---

Create a new API endpoint with the full stack:

1. **Route**: `src/routes/{resource}.routes.ts` — Express route definitions
2. **Controller**: `src/controllers/{resource}.controller.ts` — Request handling
3. **Service**: `src/services/{resource}.service.ts` — Business logic
4. **Repository**: `src/repositories/{resource}.repository.ts` — Database access
5. **Schema**: `src/schemas/{resource}.schema.ts` — Zod validation schemas
6. **Types**: `src/types/{resource}.types.ts` — TypeScript interfaces
7. **Tests**: `src/__tests__/{resource}.test.ts` — API integration tests

Follow the patterns in:
- #file:src/routes/users.routes.ts
- #file:src/controllers/users.controller.ts
- #file:src/services/users.service.ts

Include proper error handling, input validation, and pagination for list endpoints.
```

---

## Using Prompt Files

### In Copilot Chat

1. Open Copilot Chat
2. Type `/` to see available prompt files
3. Select the prompt you want to use
4. Add any additional context (e.g., "component name: SearchBar")
5. Press Enter

### With Variables

Prompt files can reference variables that you fill in when invoking them. Use curly braces `{variableName}` as placeholders and provide values when you run the prompt.

---

## Sharing Prompt Files with Your Team

Since prompt files live in `.github/prompts/`, they are **version controlled**:

- Every team member gets the same prompts
- Changes are reviewed through PRs
- New team members immediately have access to workflows
- Prompts evolve with the project

---

## Tips for Good Prompt Files

1. **Include a description** in the frontmatter for discoverability
2. **Reference existing files** with `#file:` so Copilot follows your patterns
3. **Be specific about output** — file paths, naming conventions, patterns
4. **Keep prompts focused** — One prompt per workflow
5. **Include acceptance criteria** — What does "done" look like?

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 10: Advanced Features](README.md) |
| Previous Lesson | [Model Selection](model-selection.md) |
| Next Lesson | [Knowledge Bases (Enterprise)](knowledge-bases.md) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
