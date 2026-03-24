# MCP Tools in Agent Mode

**Module 05, Lesson 3 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

The **Model Context Protocol (MCP)** extends agent mode's capabilities beyond your local filesystem and terminal. With MCP, you can give Copilot access to databases, APIs, cloud services, design tools, and more — all through standardized tool integrations.

---

## What is MCP?

MCP (Model Context Protocol) is an **open standard** that allows AI models to interact with external tools and data sources through a unified protocol. Think of it as a plugin system for AI agents.

```
┌─────────────────────────────────────────┐
│         Copilot Agent Mode               │
│                                          │
│   ┌──────────┐  ┌──────────┐            │
│   │ File Edit │  │ Terminal  │            │
│   └──────────┘  └──────────┘            │
│                                          │
│   ┌──────────────────────────┐          │
│   │     MCP Tools Layer       │          │
│   ├──────────┬───────────────┤          │
│   │ Database │ GitHub API    │          │
│   │ Server   │ Server        │          │
│   ├──────────┼───────────────┤          │
│   │ Figma    │ Slack         │          │
│   │ Server   │ Server        │          │
│   ├──────────┼───────────────┤          │
│   │ Docker   │ Custom        │          │
│   │ Server   │ Server        │          │
│   └──────────┴───────────────┘          │
└─────────────────────────────────────────┘
```

---

## Enabling MCP in VS Code

### Step 1: Enable MCP in Settings

```json
{
  "chat.mcp.enabled": true
}
```

### Step 2: Configure MCP Servers

MCP servers are configured in your VS Code settings or workspace settings. There are two methods:

### Method A: User Settings (Global)

Add to your `settings.json`:

```json
{
  "mcp": {
    "servers": {
      "github": {
        "command": "npx",
        "args": ["-y", "@modelcontextprotocol/server-github"],
        "env": {
          "GITHUB_PERSONAL_ACCESS_TOKEN": "ghp_xxxx"
        }
      },
      "postgres": {
        "command": "npx",
        "args": ["-y", "@modelcontextprotocol/server-postgres"],
        "env": {
          "DATABASE_URL": "postgresql://user:pass@localhost:5432/mydb"
        }
      }
    }
  }
}
```

### Method B: Workspace Configuration

Create a `.vscode/mcp.json` file in your project:

```json
{
  "servers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/data"]
    },
    "sqlite": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-sqlite", "database.db"]
    }
  }
}
```

---

## Popular MCP Servers

| Server | Purpose | Package |
|--------|---------|---------|
| **GitHub** | Issues, PRs, repositories | `@modelcontextprotocol/server-github` |
| **PostgreSQL** | Query and modify databases | `@modelcontextprotocol/server-postgres` |
| **SQLite** | Local database access | `@modelcontextprotocol/server-sqlite` |
| **Filesystem** | Extended file operations | `@modelcontextprotocol/server-filesystem` |
| **Brave Search** | Web search integration | `@modelcontextprotocol/server-brave-search` |
| **Puppeteer** | Browser automation | `@modelcontextprotocol/server-puppeteer` |
| **Docker** | Container management | Community server |
| **Figma** | Design file access | Community server |
| **Slack** | Message and channel access | Community server |
| **Linear** | Issue tracking | Community server |
| **Sentry** | Error monitoring | Community server |
| **Notion** | Document access | Community server |

---

## Using MCP Tools in Agent Mode

Once configured, MCP tools appear automatically in agent mode. Copilot will use them when relevant to your task.

### Example: Database-Driven Development

```
Configure your postgres MCP server, then ask:

"Look at the users table in my database and create a TypeScript
 interface that matches the schema. Then build a CRUD service
 using the Prisma ORM to interact with this table."
```

Agent mode will:
1. Use the Postgres MCP tool to query `INFORMATION_SCHEMA`
2. Read the column names, types, and constraints
3. Generate matching TypeScript interfaces
4. Create the Prisma schema
5. Build the CRUD service

### Example: GitHub Integration

```
"Check the open issues in our repository labeled 'bug'.
 Pick the easiest one and implement a fix."
```

Agent mode will:
1. Use the GitHub MCP tool to list open bug issues
2. Analyze each issue for complexity
3. Select the most straightforward one
4. Implement the fix
5. Run tests to verify

---

## MCP Security Considerations

| Concern | Recommendation |
|---------|---------------|
| API keys in settings | Use environment variables, not hardcoded keys |
| Database access | Use read-only credentials when possible |
| Network access | Only enable MCP servers you trust |
| Data exposure | Be aware of what data MCP servers can access |
| Workspace configs | Do not commit `.vscode/mcp.json` with secrets to Git |

### .gitignore Entry

```
# MCP configuration with secrets
.vscode/mcp.json
```

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 05: Edits & Agent Mode](README.md) |
| Previous Lesson | [Agent Mode](agent-mode.md) |
| Next Module | [Module 06: GitHub Copilot CLI](../06-copilot-cli/) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
