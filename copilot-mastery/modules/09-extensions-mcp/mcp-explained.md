# Model Context Protocol (MCP) Explained

**Module 09, Lesson 2 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

The **Model Context Protocol (MCP)** is an open standard — originally developed by Anthropic and now widely adopted — that defines how AI models communicate with external tools and data sources. GitHub Copilot's agent mode uses MCP to access tools beyond file editing and terminal commands.

---

## What Problem Does MCP Solve?

Before MCP, every AI tool needed custom integrations:

```
WITHOUT MCP:
  AI Tool A ──custom code──► Database
  AI Tool A ──custom code──► Slack
  AI Tool A ──custom code──► GitHub
  AI Tool B ──custom code──► Database  (different implementation!)
  AI Tool B ──custom code──► Slack     (different implementation!)

WITH MCP:
  AI Tool A ──MCP──► MCP Server (Database)
  AI Tool A ──MCP──► MCP Server (Slack)
  AI Tool B ──MCP──► MCP Server (Database)  (same server!)
  AI Tool B ──MCP──► MCP Server (Slack)     (same server!)
```

MCP provides a **universal protocol** so that tool integrations are built once and work everywhere.

---

## MCP Architecture

```
┌──────────────┐         ┌──────────────┐         ┌──────────────┐
│   Copilot    │         │  MCP Server  │         │   External   │
│   (Client)   │◄──MCP──►│  (Bridge)    │◄───────►│   Service    │
└──────────────┘         └──────────────┘         └──────────────┘

Client: Copilot agent mode in VS Code
Server: A process that exposes tools via the MCP protocol
Service: The actual external service (database, API, etc.)
```

### MCP Concepts

| Concept | Description |
|---------|-------------|
| **Client** | The AI tool (Copilot) that consumes MCP tools |
| **Server** | A process that exposes tools, resources, and prompts |
| **Tools** | Functions the AI can call (e.g., `query_database`, `send_message`) |
| **Resources** | Data the AI can read (e.g., database schemas, file listings) |
| **Prompts** | Pre-defined prompt templates the server provides |

---

## MCP Server Types

### stdio Servers (Most Common)

The server runs as a local process communicating via standard input/output:

```json
{
  "mcp": {
    "servers": {
      "sqlite": {
        "command": "npx",
        "args": ["-y", "@modelcontextprotocol/server-sqlite", "mydb.sqlite"]
      }
    }
  }
}
```

### SSE Servers (Remote)

The server runs remotely and communicates via Server-Sent Events:

```json
{
  "mcp": {
    "servers": {
      "remote-api": {
        "url": "https://mcp.example.com/sse",
        "headers": {
          "Authorization": "Bearer your-token"
        }
      }
    }
  }
}
```

### Streamable HTTP Servers

The newest transport, using HTTP with streaming:

```json
{
  "mcp": {
    "servers": {
      "cloud-service": {
        "url": "https://mcp.example.com/mcp",
        "transport": "streamable-http"
      }
    }
  }
}
```

---

## How Copilot Uses MCP Tools

When agent mode is active and MCP servers are configured:

1. **Copilot discovers tools** — Reads the available tools from each MCP server
2. **Copilot decides which tool to use** — Based on your request and available tools
3. **User approval** — You are asked to approve the tool call (configurable)
4. **Tool execution** — The MCP server executes the function
5. **Result returned** — Copilot receives the result and continues its work

### Example Flow

```
You: "Check our database for users who signed up in the last 7 days
      and create a report component showing this data."

Copilot thinks:
  1. I need to query the database → use postgres MCP tool
  2. I need to create a React component → use file editing

Copilot calls: postgres.query("SELECT * FROM users WHERE created_at > NOW() - INTERVAL '7 days'")

[You approve the tool call]

Copilot receives: [{ id: 1, name: "Alice", ... }, { id: 2, name: "Bob", ... }]

Copilot then: Creates a React component that displays this data in a table
```

---

## The MCP Ecosystem

The MCP ecosystem is growing rapidly. Key repositories:

| Resource | Description |
|----------|-------------|
| **Official Servers** | github.com/modelcontextprotocol/servers |
| **MCP Specification** | spec.modelcontextprotocol.io |
| **TypeScript SDK** | For building servers in TypeScript |
| **Python SDK** | For building servers in Python |
| **Community Servers** | Third-party servers on GitHub and npm |

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 09: Extensions & MCP](README.md) |
| Previous Lesson | [Extensions Marketplace](extensions-marketplace.md) |
| Next Lesson | [Configuring MCP Servers](configuring-mcp-servers.md) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
