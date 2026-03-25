# CLAUDE.md Templates

**Claude Code Mastery — March 2026**
**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Template 1: Node.js / TypeScript Project

```markdown
# CLAUDE.md

## Project Overview
This is a Node.js/TypeScript project using [framework].

## Tech Stack
- Runtime: Node.js 20+
- Language: TypeScript 5.x (strict mode)
- Package manager: npm (use `npm ci` for installs)
- Test framework: Jest
- Linter: ESLint + Prettier

## Commands
- Build: `npm run build`
- Test: `npm test`
- Lint: `npm run lint`
- Format: `npm run format`
- Dev server: `npm run dev`

## Code Conventions
- Use named exports, no default exports
- Prefer `async/await` over raw promises
- All functions must have JSDoc comments
- Use `interface` over `type` for object shapes
- File naming: kebab-case (e.g., `user-service.ts`)
- Max file length: 300 lines

## Project Structure
- `src/` — Application source code
- `src/routes/` — API route handlers
- `src/services/` — Business logic
- `src/models/` — Data models and types
- `tests/` — Test files mirroring src structure
```

## Template 2: Python Project

```markdown
# CLAUDE.md

## Project Overview
Python application using [framework]. Python 3.12+.

## Setup
- Virtual env: `python -m venv .venv && source .venv/bin/activate`
- Install: `pip install -e ".[dev]"`

## Commands
- Test: `pytest -v`
- Lint: `ruff check .`
- Format: `ruff format .`
- Type check: `mypy src/`

## Code Conventions
- Follow PEP 8 and PEP 257 (docstrings)
- Use type hints on all function signatures
- Prefer dataclasses or Pydantic models over plain dicts
- Use `pathlib.Path` instead of `os.path`
- Imports: stdlib, third-party, local (separated by blank lines)
- Max function length: 30 lines

## Project Structure
- `src/` — Main package
- `tests/` — Pytest test files
- `pyproject.toml` — Project configuration
```

## Template 3: Go Project

```markdown
# CLAUDE.md

## Project Overview
Go service using standard library and [framework]. Go 1.22+.

## Commands
- Build: `go build ./...`
- Test: `go test ./... -v`
- Lint: `golangci-lint run`
- Run: `go run cmd/server/main.go`

## Code Conventions
- Follow Effective Go and Go Code Review Comments
- Use `errors.New` / `fmt.Errorf` with `%w` for wrapping
- Table-driven tests with `t.Run` subtests
- No `init()` functions — prefer explicit initialization
- Context as first parameter in functions that need it
- Package names: short, lowercase, no underscores

## Project Structure
- `cmd/` — Application entry points
- `internal/` — Private packages
- `pkg/` — Public reusable packages
- `api/` — API definitions (proto, OpenAPI)
```

## Template 4: React / Next.js Project

```markdown
# CLAUDE.md

## Project Overview
React application built with Next.js 14+ (App Router).

## Commands
- Dev: `npm run dev`
- Build: `npm run build`
- Test: `npm test`
- Lint: `npm run lint`

## Code Conventions
- Functional components only (no class components)
- Use React Server Components by default, add "use client" only when needed
- State management: React Context + hooks (no Redux)
- Styling: Tailwind CSS with `cn()` utility for conditional classes
- File naming: PascalCase for components, kebab-case for utilities
- Co-locate tests: `Component.test.tsx` next to `Component.tsx`

## Project Structure
- `app/` — Next.js App Router pages and layouts
- `components/` — Reusable UI components
- `components/ui/` — Base design system components
- `lib/` — Utility functions and shared logic
- `hooks/` — Custom React hooks
```

## Template 5: Monorepo

```markdown
# CLAUDE.md — Monorepo managed with [Turborepo/Nx/pnpm workspaces]

## Commands
- Install: `pnpm install` | Build all: `pnpm run build` | Test all: `pnpm run test`
- Build specific: `pnpm --filter @scope/package-name build`

## Workspace Structure
- `apps/web` — Frontend | `apps/api` — Backend
- `packages/shared` — Shared types | `packages/ui` — Component library

## Rules
- Never import directly between apps — use packages
- Use workspace protocol: `"@scope/shared": "workspace:*"`
```

## Template 6: REST API Project

```markdown
# CLAUDE.md — REST API with auth and database

## Commands
- Dev: `npm run dev` | Test: `npm test` | Migrate: `npm run db:migrate`

## API Conventions
- URLs: `/api/v1/resources/:id` | Methods: GET, POST, PUT, DELETE
- Response: `{ "data": ..., "error": null }`
- Status codes: 200, 201, 400, 401, 404, 500

## Database
- ORM: Prisma | Migrations must be reversible | Use transactions for multi-table ops

## Structure
- `src/routes/` — Routes | `src/controllers/` — Handlers | `src/services/` — Logic
- `src/middleware/` — Auth, validation | `src/models/` — DB models | `prisma/` — Schema
```

---

> **Usage:** Copy the relevant template into a `CLAUDE.md` file at your project root and customize the placeholders in brackets.
