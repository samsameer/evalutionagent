# Build a Full-Stack App

**Module 12, Lesson 1 — Claude Code Mastery**

**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Overview

This lesson walks through building a complete task management application using Claude Code as your development partner. You will see the exact prompts to use at each stage — from project scaffolding to deployment preparation. The goal is not just to build the app, but to learn a repeatable workflow for prompt-driven full-stack development.

---

## Step 1: Project Setup

Start a new Claude Code session and scaffold the project:

```
Create a new Next.js 14 app with TypeScript, Tailwind CSS, and the App Router.
Use src/ directory structure. Add ESLint and Prettier configs.
Name the project "taskflow".
```

After Claude Code creates the project, verify the structure and add project memory:

```
Create a CLAUDE.md file for this project. It should note that we use Next.js 14
App Router with TypeScript, Tailwind for styling, PostgreSQL for the database,
and Prisma as the ORM. Tests go in __tests__/ directories next to the code they test.
```

---

## Step 2: Database Setup

With the project scaffolded, set up the database layer:

```
Add a PostgreSQL connection using Prisma. Create a schema with these models:
- User: id, email (unique), name, passwordHash, createdAt
- Task: id, title, description (optional), status (enum: TODO, IN_PROGRESS, DONE),
  priority (enum: LOW, MEDIUM, HIGH), createdAt, updatedAt, userId (relation to User)
Generate the Prisma client and create a db utility file at src/lib/db.ts.
```

Claude Code will create the Prisma schema, install dependencies, and generate the client. Run the migration:

```
Create the initial Prisma migration and apply it to my local PostgreSQL database.
The database URL is postgresql://localhost:5432/taskflow.
```

---

## Step 3: API Routes

Build the backend API using Next.js route handlers:

```
Create CRUD API routes for tasks at src/app/api/tasks/route.ts and
src/app/api/tasks/[id]/route.ts. Include:
- GET /api/tasks — list all tasks for the authenticated user, with optional
  status and priority query filters
- POST /api/tasks — create a new task
- GET /api/tasks/[id] — get a single task
- PUT /api/tasks/[id] — update a task
- DELETE /api/tasks/[id] — delete a task
Add proper error handling, input validation with Zod, and return appropriate
HTTP status codes.
```

Then add the user endpoints:

```
Create API routes for user registration and profile at src/app/api/users/route.ts.
POST should create a new user with email and password (hash the password with bcrypt).
GET should return the current user's profile.
```

---

## Step 4: Authentication

Add JWT-based authentication:

```
Add JWT authentication to the app:
1. Create a POST /api/auth/login route that accepts email and password,
   verifies credentials, and returns a JWT token
2. Create a middleware at src/middleware.ts that protects all /api/ routes
   except /api/auth/login and POST /api/users
3. Create a utility at src/lib/auth.ts with functions for generating tokens,
   verifying tokens, and extracting the user ID from a request
4. Use jose library for JWT operations. Token should expire in 24 hours.
```

Test the auth flow:

```
Create a quick test script at scripts/test-auth.sh that uses curl to:
1. Register a new user
2. Log in and capture the token
3. Create a task with the token
4. List tasks with the token
```

---

## Step 5: Frontend

Build the UI components:

```
Build the frontend UI with these pages and components:
1. src/app/page.tsx — landing page with login/register forms
2. src/app/dashboard/page.tsx — main task dashboard showing tasks in columns
   by status (TODO, IN_PROGRESS, DONE) like a Kanban board
3. src/components/TaskCard.tsx — individual task card with title, priority badge,
   and action buttons
4. src/components/TaskForm.tsx — modal form for creating and editing tasks
5. src/components/Header.tsx — navigation header with user info and logout button
Use Tailwind CSS for all styling. Store the JWT token in localStorage and include
it in API requests via a fetch wrapper at src/lib/api.ts.
```

Add interactivity:

```
Add drag-and-drop to the Kanban board so users can move tasks between status
columns. Use @hello-pangea/dnd library. When a task is dropped in a new column,
call the PUT /api/tasks/[id] endpoint to update its status.
```

---

## Step 6: Testing

Write tests across the stack:

```
Write tests for the task management app:
1. Unit tests for src/lib/auth.ts — token generation, verification, and expiry
2. API integration tests for /api/tasks routes — test CRUD operations,
   authentication enforcement, and input validation errors
3. Component tests for TaskCard and TaskForm using React Testing Library
Use Jest and React Testing Library. Create a test setup file that mocks the
Prisma client. Put tests in __tests__/ directories next to the source files.
```

Run tests and fix issues:

```
Run the test suite with npm test. If any tests fail, fix them. Make sure all
tests pass before we proceed.
```

---

## Step 7: Deployment Preparation

Prepare the app for production:

```
Prepare this app for deployment:
1. Add a Dockerfile with multi-stage build (deps, build, production)
2. Create a docker-compose.yml with the app and PostgreSQL services
3. Add a .env.example file documenting all required environment variables
4. Create a health check endpoint at /api/health that checks the database
   connection
5. Add rate limiting to the auth routes using an in-memory store
6. Update next.config.js with production security headers
```

---

## The Complete Workflow Pattern

The prompts above follow a repeatable pattern for any full-stack project:

| Stage | What to Prompt | Why |
|-------|---------------|-----|
| Scaffold | Framework, tools, directory structure | Establish the foundation with consistent conventions |
| Data layer | Models, relations, migrations | Define the domain before writing logic |
| API | Routes, validation, error handling | Build the contract between frontend and backend |
| Auth | Login, tokens, middleware | Secure the API before building the UI |
| Frontend | Pages, components, state | Build against a working backend |
| Testing | Unit, integration, component | Verify everything works together |
| Deployment | Docker, env vars, health checks | Make it production-ready |

Each prompt builds on the previous step. Claude Code maintains context about what has been created, so later prompts can reference earlier work naturally.

---

## Navigation

| Direction | Link |
|-----------|------|
| Next Lesson | [Automated Code Review Pipeline](code-review-pipeline.md) |
| Module Overview | [Module 12: Real-World Projects](README.md) |

---

> **Workflow Tip:** If your session runs long, use `/compact` between major steps to free context space. Claude Code's memory system (CLAUDE.md) ensures it remembers the project structure even after compaction.
