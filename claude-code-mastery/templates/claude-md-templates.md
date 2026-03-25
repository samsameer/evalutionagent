# CLAUDE.md Templates

**Claude Code Mastery — March 2026**
**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Template 1: Node.js / TypeScript Project

```markdown
# CLAUDE.md — Node.js/TypeScript project using [framework]

## Tech Stack
- Node.js 20+ | TypeScript 5.x (strict) | npm | Jest | ESLint + Prettier

## Commands
- Build: `npm run build` | Test: `npm test` | Lint: `npm run lint` | Dev: `npm run dev`

## Conventions
- Named exports only | `async/await` over promises | JSDoc on all functions
- `interface` over `type` for objects | kebab-case files | Max 300 lines/file

## Structure
- `src/` — Source | `src/routes/` — Handlers | `src/services/` — Logic
- `src/models/` — Types | `tests/` — Mirrors src structure
```

## Template 2: Python Project

```markdown
# CLAUDE.md — Python application using [framework]. Python 3.12+.

## Setup
- `python -m venv .venv && source .venv/bin/activate && pip install -e ".[dev]"`

## Commands
- Test: `pytest -v` | Lint: `ruff check .` | Format: `ruff format .` | Types: `mypy src/`

## Conventions
- PEP 8 + PEP 257 | Type hints on all signatures | Pydantic over dicts
- `pathlib.Path` over `os.path` | Max 30 lines/function

## Structure
- `src/` — Main package | `tests/` — Pytest files | `pyproject.toml` — Config
```

## Template 3: Go Project

```markdown
# CLAUDE.md — Go service using [framework]. Go 1.22+.

## Commands
- Build: `go build ./...` | Test: `go test ./... -v` | Lint: `golangci-lint run`

## Conventions
- Follow Effective Go | `fmt.Errorf` with `%w` | Table-driven tests with `t.Run`
- No `init()` | Context as first param | Short lowercase package names

## Structure
- `cmd/` — Entry points | `internal/` — Private | `pkg/` — Public | `api/` — Definitions
```

## Template 4: React / Next.js Project

```markdown
# CLAUDE.md — React with Next.js 14+ (App Router)

## Commands
- Dev: `npm run dev` | Build: `npm run build` | Test: `npm test` | Lint: `npm run lint`

## Conventions
- Functional components only | Server Components by default, "use client" when needed
- Tailwind CSS with `cn()` | PascalCase components | Co-locate tests next to components

## Structure
- `app/` — Pages/layouts | `components/` — UI | `lib/` — Utils | `hooks/` — Custom hooks
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
