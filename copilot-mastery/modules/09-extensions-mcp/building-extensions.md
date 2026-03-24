# Building Custom Extensions

**Module 09, Lesson 4 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

You can build your own Copilot Extensions and MCP servers to integrate custom tools, internal APIs, and proprietary systems into Copilot's workflow.

---

## Option 1: Build an MCP Server

MCP servers are the easiest way to extend Copilot's agent mode.

### TypeScript MCP Server Example

```bash
mkdir my-mcp-server && cd my-mcp-server
npm init -y
npm install @modelcontextprotocol/sdk
```

```typescript
// src/index.ts
import { McpServer } from "@modelcontextprotocol/sdk/server/mcp.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";

const server = new McpServer({
  name: "my-custom-tools",
  version: "1.0.0",
});

// Define a tool
server.tool(
  "get_weather",
  "Get current weather for a city",
  {
    city: { type: "string", description: "City name" },
  },
  async ({ city }) => {
    // Your implementation here
    const weather = await fetchWeather(city);
    return {
      content: [
        {
          type: "text",
          text: JSON.stringify(weather, null, 2),
        },
      ],
    };
  }
);

// Define a resource
server.resource(
  "config",
  "app://config",
  async () => ({
    contents: [
      {
        uri: "app://config",
        mimeType: "application/json",
        text: JSON.stringify({ version: "1.0", environment: "dev" }),
      },
    ],
  })
);

// Start the server
const transport = new StdioServerTransport();
await server.connect(transport);
```

### Python MCP Server Example

```bash
pip install mcp
```

```python
# server.py
from mcp.server import Server
from mcp.server.stdio import stdio_server

app = Server("my-custom-tools")

@app.tool()
async def get_weather(city: str) -> str:
    """Get current weather for a city."""
    # Your implementation here
    return f"Weather in {city}: 25°C, Sunny"

@app.tool()
async def search_internal_docs(query: str) -> str:
    """Search internal documentation."""
    # Connect to your internal search system
    results = await internal_search(query)
    return results

async def main():
    async with stdio_server() as (read_stream, write_stream):
        await app.run(read_stream, write_stream)

if __name__ == "__main__":
    import asyncio
    asyncio.run(main())
```

### Register Your MCP Server in VS Code

```json
{
  "servers": {
    "my-tools": {
      "command": "node",
      "args": ["path/to/my-mcp-server/dist/index.js"]
    }
  }
}
```

---

## Option 2: Build a Copilot Extension (GitHub App)

For extensions that appear on GitHub.com and in the marketplace:

### Architecture

```
GitHub.com / VS Code
       │
       ▼
  Copilot Extension API
       │
       ▼
  Your Server (handles requests)
       │
       ▼
  Your Backend / External APIs
```

### Steps to Build

1. **Create a GitHub App** at github.com/settings/apps
2. **Enable Copilot Extension** in the app settings
3. **Implement the webhook endpoint** that handles Copilot requests
4. **Deploy your server** (any hosting platform)
5. **Publish** to the GitHub Marketplace (optional)

### Request/Response Format

Your server receives messages in this format:

```json
{
  "messages": [
    {
      "role": "user",
      "content": "@your-extension What's the status of project Alpha?"
    }
  ],
  "copilot_references": [...],
  "copilot_thread_id": "thread-123"
}
```

And responds with:

```json
{
  "choices": [
    {
      "message": {
        "role": "assistant",
        "content": "Project Alpha is on track. Sprint velocity: 42 points..."
      }
    }
  ]
}
```

---

## When to Build What

| Build This | When You Need |
|-----------|--------------|
| **MCP Server** | Tools for agent mode, database access, local integrations |
| **Copilot Extension** | Chat participant on GitHub.com, marketplace distribution |
| **Both** | Full integration across VS Code agent mode AND GitHub.com chat |

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 09: Extensions & MCP](README.md) |
| Previous Lesson | [Configuring MCP Servers](configuring-mcp-servers.md) |
| Next Module | [Module 10: Advanced Features](../10-advanced-features/) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
