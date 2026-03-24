# Custom Instructions Examples

**GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Ready-to-use `.github/copilot-instructions.md` templates for different project types. Copy the one that matches your stack and customize it.

---

## Template 1: React + TypeScript Frontend

```markdown
# Copilot Instructions

## Language & Framework
- TypeScript strict mode, React 19
- Functional components only, no class components
- Use React hooks (useState, useEffect, useMemo, useCallback)
- Use React Server Components where appropriate (Next.js)

## Styling
- Tailwind CSS v4 for all styling
- No inline styles, no CSS modules
- Mobile-first responsive design
- Use cn() utility from lib/utils for conditional classes

## State Management
- Zustand for global state
- React Query (TanStack Query) for server state
- Local state (useState) for component-specific state

## Conventions
- Named exports only, no default exports
- File naming: kebab-case (user-profile.tsx)
- Component naming: PascalCase (UserProfile)
- Props interface: [ComponentName]Props

## Do Not
- Do not use `any` type — use `unknown` and narrow
- Do not use `console.log` — use the logger utility
- Do not use inline event handlers for complex logic
- Do not use index as key in lists
```

---

## Template 2: Node.js + Express Backend

```markdown
# Copilot Instructions

## Language & Framework
- TypeScript strict mode, Node.js 20, Express.js
- ES modules (import/export), no CommonJS

## Architecture
- Clean architecture: routes → controllers → services → repositories
- All files in src/ with subdirectories by layer
- Dependency injection via constructor parameters

## Database
- Prisma ORM for all database access
- Never write raw SQL unless Prisma cannot express the query
- All queries through repository classes

## Validation
- Zod for all input validation at route level
- Validate before passing to controllers
- Return 400 with specific error messages

## Error Handling
- Use custom AppError class from src/errors/
- Centralized error handling middleware
- Log all errors with the logger from src/utils/logger
- Never catch and swallow errors silently

## Testing
- Jest for unit tests, Supertest for API tests
- Tests alongside source files: *.test.ts
- Mock database with Prisma mock client
- 80% code coverage minimum
```

---

## Template 3: Python + FastAPI Backend

```markdown
# Copilot Instructions

## Language & Framework
- Python 3.12+, FastAPI
- Use Pydantic v2 models for request/response validation
- Use async/await for all I/O operations

## Architecture
- app/routers/ for API endpoints
- app/services/ for business logic
- app/models/ for SQLAlchemy models
- app/schemas/ for Pydantic schemas
- app/dependencies/ for dependency injection

## Database
- SQLAlchemy 2.0 with async support
- Alembic for migrations
- Never use raw SQL in application code

## Code Style
- Follow PEP 8 and PEP 484 (type hints)
- Use pathlib for file paths, not os.path
- Use f-strings for string formatting
- Use dataclasses or Pydantic for data structures

## Testing
- pytest with pytest-asyncio
- httpx.AsyncClient for API tests
- Factory Boy for test data factories
- 80% coverage minimum
```

---

## Template 4: Go API Service

```markdown
# Copilot Instructions

## Language
- Go 1.22+, standard library preferred
- Only add external dependencies when absolutely necessary

## Architecture
- cmd/ for entry points
- internal/ for private packages
- pkg/ for public packages
- Handler → Service → Repository pattern

## Conventions
- Follow standard Go conventions (gofmt, go vet)
- Error handling: always check and handle errors
- Use context.Context for cancellation and timeouts
- Interfaces in the consumer package, not the provider

## Testing
- Standard library testing package
- Table-driven tests with subtests
- Use testify/assert only for complex assertions
- Mock interfaces, not concrete types

## Do Not
- Do not use init() functions
- Do not use global variables for state
- Do not panic in library code
- Do not use interface{}/any when a specific type works
```

---

## Template 5: Full-Stack Monorepo

```markdown
# Copilot Instructions

## Monorepo Structure
- apps/web/ — Next.js frontend
- apps/api/ — Express.js backend
- packages/shared/ — Shared types and utilities
- packages/ui/ — Shared UI components

## Shared Rules
- TypeScript strict mode everywhere
- Use shared types from packages/shared
- Never duplicate types between apps

## Frontend (apps/web)
- Next.js 14 App Router
- Tailwind CSS, React Server Components
- TanStack Query for data fetching

## Backend (apps/api)
- Express.js with Zod validation
- Prisma ORM, PostgreSQL
- JWT authentication

## Testing
- Vitest for unit tests
- Playwright for E2E tests
- Each package has its own test suite
```

---

## How to Use These Templates

1. Choose the template closest to your project
2. Create `.github/copilot-instructions.md` in your repo
3. Paste the template content
4. Customize the specific libraries, patterns, and conventions
5. Commit to your repository
6. Copilot automatically uses these instructions

---

## Navigation

| Direction | Link |
|-----------|------|
| Templates Home | [Templates](../templates/) |
| Course Home | [GitHub Copilot Mastery](../README.md) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
