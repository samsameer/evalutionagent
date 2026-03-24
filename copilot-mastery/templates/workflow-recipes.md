# Workflow Recipes

**GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Step-by-step recipes for common development workflows using GitHub Copilot features.

---

## Recipe 1: New Feature Development

### Ingredients
- Copilot Chat (Ask mode)
- Agent Mode
- Inline Completions
- Copilot Edits

### Steps

1. **Plan** — Open Chat Panel, ask:
   ```
   @workspace I need to add [feature]. What files would need to change?
   What's the best approach given the current architecture?
   ```

2. **Scaffold** — Switch to Agent Mode:
   ```
   Create the initial structure for [feature] following the plan above.
   Create the files, add types/interfaces, and stub out functions.
   ```

3. **Implement** — Use inline completions to write the logic, letting Copilot suggest as you type

4. **Refactor** — Use Copilot Edits to adjust multiple files:
   ```
   Update all files in the working set to handle the new
   [feature] error cases consistently.
   ```

5. **Test** — Switch to Agent Mode:
   ```
   Write tests for the [feature] I just implemented.
   Run them and fix any failures.
   ```

6. **Review** — Ask Copilot Chat:
   ```
   @workspace Review my changes for potential issues, security
   vulnerabilities, and missed edge cases.
   ```

---

## Recipe 2: Bug Fix Workflow

### Steps

1. **Understand** — Paste the bug report into Chat:
   ```
   Here's a bug report: [paste]. Where in the codebase
   might this issue originate?
   ```

2. **Locate** — Use @workspace:
   ```
   @workspace Find the code responsible for [behavior]
   ```

3. **Fix** — Use Inline Chat (`Ctrl+I`) on the buggy code:
   ```
   Fix: [describe the expected behavior]
   ```

4. **Regression Test** — In Chat:
   ```
   /tests Write a regression test that would have caught this bug
   ```

5. **Verify** — Agent Mode:
   ```
   Run all tests and confirm they pass
   ```

---

## Recipe 3: Code Review Acceleration

### Steps

1. **Understand the PR** — In Chat:
   ```
   #changes Summarize what these changes do and why
   ```

2. **Check for issues** — In Chat:
   ```
   #changes Review for: security issues, performance problems,
   missing error handling, and code quality
   ```

3. **Verify tests** — In Chat:
   ```
   #changes Are the test changes adequate? What edge cases are missing?
   ```

4. **Write review comments** — Use Chat to draft constructive feedback

---

## Recipe 4: Learning a New Codebase

### Steps

1. **Overview**:
   ```
   @workspace Give me a high-level overview of this project.
   What does it do, what tech stack does it use, and how is it organized?
   ```

2. **Architecture**:
   ```
   @workspace Draw the architecture — what are the main components
   and how do they communicate?
   ```

3. **Entry points**:
   ```
   @workspace Where is the main entry point? Walk me through
   what happens when a request comes in.
   ```

4. **Key patterns**:
   ```
   @workspace What design patterns does this project use?
   Show me examples.
   ```

5. **Run it**:
   ```
   @workspace How do I build and run this project locally?
   What environment variables do I need?
   ```

---

## Recipe 5: Database Schema Changes

### Steps

1. **Design** — In Chat:
   ```
   I need to add [feature]. What database schema changes are needed?
   Consider: data types, indexes, foreign keys, and migration safety.
   ```

2. **Migrate** — Agent Mode:
   ```
   Create a Prisma migration that adds [changes].
   Generate the migration and apply it to the dev database.
   ```

3. **Update Code** — Agent Mode:
   ```
   Update the service layer and API routes to support
   the new schema. Update relevant tests.
   ```

4. **Verify** — Agent Mode:
   ```
   Run all tests and the type checker to ensure
   nothing is broken.
   ```

---

## Recipe 6: API Documentation Generation

### Steps

1. **Generate** — In Chat:
   ```
   @workspace Generate OpenAPI/Swagger documentation for all
   API endpoints in this project. Include request/response schemas,
   authentication requirements, and example values.
   ```

2. **Review** — Verify the generated docs match actual behavior

3. **Serve** — Agent Mode:
   ```
   Add Swagger UI to serve the API docs at /api/docs
   ```

---

## Navigation

| Direction | Link |
|-----------|------|
| Templates Home | [Templates](../templates/) |
| Course Home | [GitHub Copilot Mastery](../README.md) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
