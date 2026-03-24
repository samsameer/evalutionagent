# Prompt Templates for GitHub Copilot

**GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Copy and paste these prompts directly into Copilot Chat for common development tasks. Replace text in `[brackets]` with your specific details.

---

## Code Generation

### Generate a React Component

```
Create a React component called [ComponentName] that:
- Uses TypeScript with proper prop types
- Accepts the following props: [list props]
- Implements [describe behavior]
- Uses Tailwind CSS for styling
- Is responsive for mobile and desktop
- Includes proper accessibility attributes (aria labels, roles)
```

### Generate an API Endpoint

```
Create a [GET/POST/PUT/DELETE] API endpoint at [/api/path] that:
- Accepts [describe input/params]
- Validates input with Zod
- Calls [describe service/database operation]
- Returns [describe response shape]
- Handles errors: [list error scenarios]
- Requires authentication: [yes/no]
```

### Generate a Database Migration

```
Create a Prisma migration that:
- Adds a new [table/column/index]: [describe]
- The [table] has these fields: [list fields with types]
- Add relationships to: [related tables]
- Add indexes on: [columns that need indexing]
- Include a seed script with sample data
```

---

## Testing

### Generate Unit Tests

```
Write comprehensive unit tests for #file:[path/to/file]:
- Test all public functions/methods
- Cover happy path scenarios
- Cover edge cases: [null, empty, boundary values, etc.]
- Test error handling and thrown exceptions
- Use [Jest/Vitest/pytest] with [describe mocking approach]
- Target 90%+ code coverage
```

### Generate Integration Tests

```
Write integration tests for the [feature/module] that:
- Test the complete flow from [start] to [end]
- Use [test database/mock server]
- Verify [specific behaviors]
- Clean up test data after each test
- Can run in CI without external dependencies
```

---

## Debugging

### Debug an Error

```
I'm getting this error:

[paste error message]

It occurs when: [describe the scenario]
Expected behavior: [what should happen]
Actual behavior: [what happens instead]

Look at #file:[relevant file] and help me fix it.
```

### Performance Issue

```
This [function/query/component] is slow:

#file:[path to slow code]

Current performance: [describe metrics]
Target performance: [describe target]
Constraints: [any constraints]

Identify the bottleneck and optimize it.
```

---

## Refactoring

### Extract and Refactor

```
Refactor #selection to:
1. Extract [describe what to extract] into a separate [function/class/module]
2. [Specific refactoring goal]
3. [Specific refactoring goal]

Keep the same public API — no breaking changes.
Add tests to verify behavior is unchanged.
```

### Modernize Code

```
Modernize #file:[path] to use current best practices:
- Replace [old pattern] with [new pattern]
- Update to [new API/syntax]
- Improve type safety
- Maintain backward compatibility
```

---

## Documentation

### Generate API Documentation

```
Generate comprehensive API documentation for #file:[path]:
- Endpoint URL and HTTP method
- Request parameters (path, query, body) with types
- Response format with example JSON
- Error responses and status codes
- Authentication requirements
- Rate limiting details
- Example curl commands
```

### Generate Code Comments

```
Add clear, concise comments to #file:[path]:
- Function-level JSDoc/docstrings with @param and @returns
- Inline comments only where logic is non-obvious
- Do not over-comment simple/self-evident code
- Explain "why" not "what"
```

---

## DevOps

### Generate GitHub Actions Workflow

```
Create a GitHub Actions workflow that:
- Triggers on: [push/PR/schedule/manual]
- Runs on: [ubuntu-latest/specific runner]
- Steps:
  1. [Step 1]
  2. [Step 2]
  3. [Step 3]
- Environment variables: [list]
- Secrets needed: [list]
- Caching: [npm/pip/cargo cache]
```

### Generate Dockerfile

```
Create a multi-stage Dockerfile for a [language/framework] application:
- Build stage: compile/build the application
- Production stage: minimal runtime image
- Use [specific base image]
- Copy only necessary files
- Set proper user permissions (non-root)
- Include health check
- Optimize for layer caching
```

---

## Agent Mode Prompts

### Scaffold a New Feature

```
Implement [feature name] for this project:

Requirements:
- [Requirement 1]
- [Requirement 2]
- [Requirement 3]

Follow the existing patterns in #file:[reference file].
Create tests for all new code.
Run the tests and fix any failures.
```

### Fix a Bug End-to-End

```
Fix this bug:

Issue: [describe the bug]
Steps to reproduce: [steps]
Expected: [expected behavior]
Actual: [actual behavior]

1. Find the root cause
2. Implement the fix
3. Add a regression test
4. Run all tests to ensure nothing is broken
```

---

## Navigation

| Direction | Link |
|-----------|------|
| Templates Home | [Templates](../templates/) |
| Course Home | [GitHub Copilot Mastery](../README.md) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
