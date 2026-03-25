# Build a Full-Stack App

**Module 12, Lesson 1 — Claude Code Mastery**

**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Overview

This lesson walks through building a full-stack task management app using Claude Code. You will see the exact prompts to use at each stage, from scaffolding through deployment prep.

---

## Step 1: Project Setup

```
Create a new Next.js 14 app with the App Router, TypeScript, Tailwind CSS,
and ESLint. Name it "taskflow". Use src/ directory structure. Initialize a
Git repo and create the first commit.
```

---

## Step 2: Database Setup

```
Add a PostgreSQL connection using Prisma ORM. Create a schema with:
- User: id, email (unique), name, passwordHash, createdAt
- Task: id, title, description (optional), status (enum: TODO, IN_PROGRESS,
  DONE), priority (enum: LOW, MEDIUM, HIGH), createdAt, updatedAt, userId
Generate the Prisma client and a seed script with 2 users and 5 tasks each.
```

```
Add a docker-compose.yml for local PostgreSQL on port 5433. Include npm
scripts for db:push, db:seed, and db:reset.
```

---

## Step 3: API Routes

```
Create CRUD API routes for tasks using Next.js route handlers:
- GET /api/tasks — list tasks for the authenticated user, support ?status filter
- POST /api/tasks — create a task
- GET /api/tasks/[id] — get one task
- PATCH /api/tasks/[id] — update a task
- DELETE /api/tasks/[id] — delete a task
Use Prisma for DB access. Validate request bodies with Zod schemas.
Return proper HTTP status codes and error messages.
```

---

## Step 4: Authentication

```
Add JWT authentication:
- POST /api/auth/register — hash password with bcrypt, return JWT
- POST /api/auth/login — verify credentials, return JWT
- Create middleware that verifies the JWT from the Authorization header
- Protect all /api/tasks routes with this middleware
- Store the JWT secret in .env and add .env to .gitignore
```

Validate the flow:

```
Walk me through the auth flow: register, log in, and create a task.
Show the curl commands I would use for each step.
```

---

## Step 5: Frontend UI

```
Build the frontend with:
- /login and /register pages with Tailwind-styled forms
- /dashboard with a Kanban board (columns: TODO, IN_PROGRESS, DONE)
- Task cards showing title, priority badge, and status dropdown
- A modal form for creating new tasks
- Store JWT in localStorage, include it in API requests via a fetch wrapper
```

Refine the experience:

```
Add loading states, error toasts with react-hot-toast, and empty state
messages. Make task cards draggable between columns using @hello-pangea/dnd.
```

---

## Step 6: Testing

```
Write tests for the application:
- Unit tests for Zod schemas using Vitest
- API integration tests for each route with supertest and a test database
- Component tests for TaskCard and CreateTaskModal with React Testing Library
Add scripts: test, test:unit, test:integration, and test:coverage.
```

```
Review the tests and add cases for unauthorized access, invalid task IDs,
and duplicate email registration.
```

---

## Step 7: Deployment Prep

```
Prepare for deployment:
- Multi-stage Dockerfile optimized for Next.js standalone output
- .env.example with all required variables documented
- Health check at GET /api/health that verifies the database connection
- Security headers in next.config.js
- README with setup instructions and architecture overview
```

---

## Prompt Pattern Summary

| Stage | Pattern | Why It Works |
|-------|---------|--------------|
| Setup | "Create a new X with Y, Z" | Specific tech choices reduce ambiguity |
| Database | "Add X using Y. Create a schema..." | Naming the ORM and listing models gives structure |
| API | "Create CRUD API for X..." | CRUD is a well-understood pattern |
| Auth | "Add JWT authentication..." | Step-by-step flow with clear requirements |
| UI | "Build the frontend with these pages..." | Page-by-page keeps scope manageable |
| Tests | "Write tests using Vitest..." | Naming the framework sets expectations |
| Deploy | "Prepare for deployment..." | Checklist format ensures completeness |

---

## Common Mistakes

| Mistake | Better Approach |
|---------|----------------|
| "Build me a task app" | Break into stages with specific prompts |
| Skipping validation | Always request Zod schemas |
| One giant prompt | One stage per prompt, verify before continuing |

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Overview | [README](README.md) |
| Next Lesson | [Automated Code Review Pipeline](code-review-pipeline.md) |

---

> **Workflow Tip:** Commit after each step. If Claude produces something unexpected later, you can roll back cleanly.
