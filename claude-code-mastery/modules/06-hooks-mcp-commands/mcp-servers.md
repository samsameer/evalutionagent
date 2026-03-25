# MCP Servers

**Module 06, Lesson 2 — Claude Code Mastery**

**Instructor: Jabbir Basha, Principal AI Engineer**

---

## What Is MCP?

The **Model Context Protocol (MCP)** is an open standard that allows AI assistants like Claude Code to communicate with external tools and data sources through a unified interface. Instead of building custom integrations for every service, MCP provides a single protocol that any server can implement.

With MCP, Claude Code can:

- Query databases directly
- Create GitHub issues and pull requests
- Send Slack messages
- Access monitoring tools like Sentry
- Interact with any service that exposes an MCP server

---

## How MCP Works in Claude Code

```
┌─────────────┐     MCP Protocol     ┌──────────────┐     API      ┌──────────┐
│ Claude Code  │ ◄──────────────────► │  MCP Server  │ ◄──────────► │ Service  │
│  (Client)    │   (JSON-RPC/stdio)   │  (Bridge)    │   (REST/DB)  │ (GitHub) │
└─────────────┘                       └──────────────┘              └──────────┘
```

Claude Code acts as the MCP **client**. MCP **servers** are lightweight processes that translate between the MCP protocol and the target service's native API.

---

## Transport Types

| Transport | Protocol | Best For | Latency |
|-----------|----------|----------|---------|
| **stdio** | stdin/stdout pipes | Local processes, CLI tools | Very low |
| **SSE** | HTTP Server-Sent Events | Remote servers, shared services | Medium |

### stdio Transport

The server runs as a child process. Claude Code communicates via stdin/stdout:

```json
{
  "mcpServers": {
    "my-server": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/dir"]
    }
  }
}
```

### SSE Transport

The server runs as an HTTP service. Claude Code connects via URL:

```json
{
  "mcpServers": {
    "remote-server": {
      "type": "sse",
      "url": "http://localhost:3001/sse"
    }
  }
}
```

---

## Configuring MCP Servers

MCP servers are configured in your settings files:

| Scope | File | Use Case |
|-------|------|----------|
| Project | `.claude/settings.json` | Project-specific servers (project DB, staging API) |
| User | `~/.claude/settings.json` | Personal servers (your GitHub token, your Slack) |

### Basic Configuration Schema

```json
{
  "mcpServers": {
    "server-name": {
      "type": "stdio",
      "command": "command-to-run",
      "args": ["arg1", "arg2"],
      "env": {
        "API_KEY": "your-key-here"
      },
      "cwd": "/optional/working/directory"
    }
  }
}
```

| Field | Required | Description |
|-------|----------|-------------|
| `type` | Yes | `"stdio"` or `"sse"` |
| `command` | Yes (stdio) | Executable to run |
| `args` | No | Command-line arguments |
| `env` | No | Environment variables for the server process |
| `cwd` | No | Working directory for the server process |
| `url` | Yes (SSE) | URL for SSE transport |

---

## Popular MCP Servers

### GitHub MCP Server

Access repositories, issues, pull requests, and code search:

```json
{
  "mcpServers": {
    "github": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "ghp_xxxxxxxxxxxx"
      }
    }
  }
}
```

**Tools exposed:** `create_issue`, `list_pull_requests`, `search_code`, `get_file_contents`, `create_pull_request`, and more.

### Slack MCP Server

Send messages, read channels, manage threads:

```json
{
  "mcpServers": {
    "slack": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@anthropic/mcp-server-slack"],
      "env": {
        "SLACK_BOT_TOKEN": "xoxb-your-token"
      }
    }
  }
}
```

### PostgreSQL MCP Server

Query databases directly from Claude Code:

```json
{
  "mcpServers": {
    "postgres": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres"],
      "env": {
        "DATABASE_URL": "postgresql://user:pass@localhost:5432/mydb"
      }
    }
  }
}
```

### Sentry MCP Server

Access error tracking and monitoring data:

```json
{
  "mcpServers": {
    "sentry": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@sentry/mcp-server"],
      "env": {
        "SENTRY_AUTH_TOKEN": "sntrys_xxxxxxxxxxxx"
      }
    }
  }
}
```

### Filesystem MCP Server

Provide controlled file access to specific directories:

```json
{
  "mcpServers": {
    "filesystem": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/home/user/data"]
    }
  }
}
```

---

## Context Cost of MCP Servers

Each connected MCP server adds to Claude's context window because the server's tool definitions are included in every request. Be mindful of this:

| Factor | Impact |
|--------|--------|
| Number of servers | Each adds tool definitions to context |
| Tools per server | More tools = more context tokens consumed |
| Tool descriptions | Verbose descriptions cost more tokens |
| Active connections | All connected servers consume context, even if unused |

**Best practices:**

1. Only enable MCP servers you actively need for the current project
2. Prefer servers with focused, minimal tool sets
3. Disable servers you are not using with the `/mcp` command
4. Use project-level config so servers only load for relevant projects

---

## The /mcp Command

Use the `/mcp` slash command inside Claude Code to manage MCP servers at runtime:

| Action | Description |
|--------|-------------|
| `/mcp` | List all configured MCP servers and their status |
| `/mcp start <name>` | Start a specific MCP server |
| `/mcp stop <name>` | Stop a running MCP server |

This lets you enable or disable servers without editing configuration files or restarting your session.

---

## Troubleshooting MCP Servers

| Problem | Solution |
|---------|----------|
| Server fails to start | Run the command manually in a terminal to see error output |
| Authentication errors | Verify tokens/credentials in the `env` configuration |
| Tools not appearing | Check `/mcp` to confirm the server is connected |
| High context usage | Reduce the number of active MCP servers |
| Timeout on startup | Increase timeout or check network connectivity (SSE) |

---

## Security Considerations

- **Never commit API tokens** to `.claude/settings.json` if it is tracked in git. Use `~/.claude/settings.json` for secrets, or reference environment variables.
- **Scope server permissions** to the minimum required (read-only GitHub tokens if you only need to read).
- **Review MCP server source code** before running third-party servers — they execute with your user permissions.

---

## Navigation

| Direction | Link |
|-----------|------|
| Previous | [Hooks System](hooks-system.md) |
| Next | [Custom Commands](custom-commands.md) |
| Module Home | [Module 06 Overview](README.md) |
