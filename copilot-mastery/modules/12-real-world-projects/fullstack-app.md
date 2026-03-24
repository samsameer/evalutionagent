# Building a Full-Stack App with Agent Mode

**Module 12, Lesson 1 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

In this project, you will build a **complete task management application** using Next.js, TypeScript, Prisma, and PostgreSQL — driven almost entirely by Copilot Agent Mode. This demonstrates the full power of agentic AI development.

---

## The Project: TaskFlow

**TaskFlow** is a task management application with:
- User authentication (NextAuth.js)
- CRUD operations for tasks
- Task categorization and tagging
- Due dates and priority levels
- Dashboard with statistics
- Responsive UI with Tailwind CSS

---

## Step 1: Scaffold the Project

Open Copilot Chat in **Agent Mode** and type:

```
Create a new Next.js 14 project called "taskflow" with:
- TypeScript strict mode
- Tailwind CSS
- Prisma ORM configured for PostgreSQL
- NextAuth.js for authentication
- A clean folder structure following Next.js app router conventions

Install all dependencies and ensure the project compiles.
```

**What Agent Mode Does:**
1. Runs `npx create-next-app@latest taskflow --typescript --tailwind --app`
2. Installs Prisma, NextAuth, and other dependencies
3. Creates `prisma/schema.prisma` with initial models
4. Configures `tsconfig.json` with strict mode
5. Runs `npx tsc` to verify compilation

---

## Step 2: Define the Database Schema

```
Create a Prisma schema with the following models:

User:
  - id, email, name, password (hashed), createdAt, updatedAt
  - Has many tasks

Task:
  - id, title, description, status (TODO/IN_PROGRESS/DONE),
    priority (LOW/MEDIUM/HIGH), dueDate, tags (string array)
  - Belongs to a user
  - createdAt, updatedAt

Generate the Prisma client and create a database migration.
```

---

## Step 3: Build the API Layer

```
Create API routes for the Task model:

- GET /api/tasks — List all tasks for the authenticated user
  (with filtering by status, priority, and search)
- POST /api/tasks — Create a new task
- GET /api/tasks/[id] — Get a specific task
- PUT /api/tasks/[id] — Update a task
- DELETE /api/tasks/[id] — Delete a task
- GET /api/tasks/stats — Get dashboard statistics
  (total, by status, overdue count)

Use Zod for input validation.
All routes require authentication.
Follow RESTful conventions.
```

---

## Step 4: Build the UI

```
Create the following pages and components:

1. Login page at /login with email and password
2. Dashboard at / showing:
   - Statistics cards (total tasks, by status, overdue)
   - Task list with filters (status, priority, search)
   - "Add Task" button
3. Task creation/edit modal with form fields
4. Individual task view at /tasks/[id]

Use Tailwind CSS for styling.
Make it responsive for mobile and desktop.
Use React Server Components where appropriate.
```

---

## Step 5: Add Tests

```
Add comprehensive tests for the TaskFlow application:

1. Unit tests for API route handlers (mock Prisma)
2. Unit tests for Zod validation schemas
3. Component tests for the task list and task form
4. Integration test for the complete create/read/update/delete flow

Use Jest and React Testing Library.
Run the tests and fix any failures.
```

---

## What You Learned

By completing this project with agent mode, you experienced:

- **Autonomous scaffolding** — Agent mode set up the entire project
- **Multi-file generation** — Created schemas, routes, components, and tests
- **Command execution** — npm install, prisma generate, tsc, jest
- **Self-correction** — Fixed compilation and test errors automatically
- **Iterative development** — Built the app in logical steps

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 12: Real-World Projects](README.md) |
| Next Lesson | [REST API with Tests](rest-api-tests.md) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
