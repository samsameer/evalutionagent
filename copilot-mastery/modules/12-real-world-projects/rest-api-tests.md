# REST API with Tests

**Module 12, Lesson 2 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

In this project, you will use a combination of Copilot features — inline completions, chat, and agent mode — to build a **production-ready REST API** with comprehensive test coverage.

---

## The Project: BookShelf API

A REST API for managing a book collection:
- CRUD operations for books
- Author management
- Search and filtering
- Pagination
- Rate limiting
- Comprehensive test suite (90%+ coverage)

---

## Workflow: Mixing Copilot Features

This project deliberately uses **different Copilot features for different tasks** to show when each is most effective.

### Phase 1: Project Setup — Agent Mode

```
Create an Express.js API with TypeScript:
- Express + TypeScript configuration
- Folder structure: routes, controllers, services, repositories, middleware
- Zod for validation
- Jest + Supertest for testing
- SQLite with Prisma for database (simple local dev)
- Install all dependencies and verify build
```

### Phase 2: Database Models — Inline Completions

Write the Prisma schema yourself, letting Copilot's **inline completions** help:

```prisma
model Book {
  id          Int      @id @default(autoincrement())
  title       String
  // Start typing and let Copilot complete the fields...
```

Copilot suggests fields based on the model name and context.

### Phase 3: Business Logic — Copilot Chat

Use `/explain` and `/fix` during implementation:

```
@workspace What's the best way to implement pagination
with Prisma that returns total count alongside results?
```

### Phase 4: Test Writing — Agent Mode

```
Write comprehensive tests for the BookShelf API:
- Test all CRUD endpoints for books and authors
- Test validation (missing fields, invalid types, too-long strings)
- Test pagination (first page, last page, out-of-range page)
- Test search functionality
- Test error cases (404, 400, 500)
- Test rate limiting

Run the tests and fix any failures.
Target 90%+ code coverage.
```

### Phase 5: Code Review — Copilot Chat

```
@workspace Review the BookShelf API for:
1. Security vulnerabilities
2. Missing error handling
3. Performance issues
4. Code quality improvements
```

---

## Key Takeaway

Different Copilot features excel at different tasks:

| Task | Best Feature |
|------|-------------|
| Project scaffolding | Agent Mode |
| Writing code | Inline Completions |
| Understanding code | Copilot Chat (/explain) |
| Fixing bugs | Copilot Chat (/fix) |
| Writing tests | Agent Mode |
| Code review | Copilot Chat (@workspace) |
| Refactoring | Copilot Edits |

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 12: Real-World Projects](README.md) |
| Previous Lesson | [Full-Stack App](fullstack-app.md) |
| Next Lesson | [CI/CD Pipeline Setup](cicd-pipeline.md) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
