# Configuring MCP Servers

**Module 09, Lesson 3 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

This lesson provides practical, step-by-step instructions for configuring MCP servers in VS Code for use with Copilot agent mode. For a deeper explanation of MCP, see [Module 05, Lesson 3](../05-copilot-edits-agent-mode/mcp-tools.md).

---

## Configuration Locations

| Location | Scope | File |
|----------|-------|------|
| **User settings** | All workspaces | VS Code `settings.json` |
| **Workspace settings** | Current workspace | `.vscode/mcp.json` |
| **Workspace settings alt** | Current workspace | `.vscode/settings.json` |

---

## Step-by-Step: PostgreSQL Server

### 1. Enable MCP

In VS Code settings:
```json
{
  "chat.mcp.enabled": true
}
```

### 2. Create `.vscode/mcp.json`

```json
{
  "servers": {
    "postgres": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres"],
      "env": {
        "DATABASE_URL": "postgresql://user:password@localhost:5432/mydb"
      }
    }
  }
}
```

### 3. Reload VS Code

Press `Ctrl+Shift+P` → "Developer: Reload Window"

### 4. Verify

Open Copilot Chat in Agent mode and type:
```
List all tables in my database
```

If configured correctly, Copilot will use the Postgres MCP tool to query your database.

---

## Step-by-Step: GitHub Server

```json
{
  "servers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "ghp_your_token_here"
      }
    }
  }
}
```

**Tools available:** Search repos, list issues, read PR details, get file contents.

---

## Step-by-Step: Filesystem Server

For projects that need broader file access:

```json
{
  "servers": {
    "filesystem": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-filesystem",
        "/Users/you/Documents/data",
        "/Users/you/Downloads"
      ]
    }
  }
}
```

---

## Step-by-Step: Brave Search Server

Add web search capability to agent mode:

```json
{
  "servers": {
    "brave-search": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-brave-search"],
      "env": {
        "BRAVE_API_KEY": "your_brave_api_key"
      }
    }
  }
}
```

---

## Step-by-Step: Puppeteer Server

Browser automation for testing and scraping:

```json
{
  "servers": {
    "puppeteer": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-puppeteer"]
    }
  }
}
```

---

## Multiple Servers Configuration

You can configure multiple servers simultaneously:

```json
{
  "servers": {
    "postgres": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres"],
      "env": { "DATABASE_URL": "postgresql://..." }
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": { "GITHUB_PERSONAL_ACCESS_TOKEN": "ghp_..." }
    },
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/data"]
    }
  }
}
```

---

## Troubleshooting MCP Servers

| Issue | Solution |
|-------|----------|
| Server not starting | Check that `npx` is available and the package exists |
| "Tool not found" | Reload VS Code after adding configuration |
| Authentication errors | Verify environment variables and tokens |
| Timeout errors | Check network connectivity to external services |
| Permission denied | Ensure the command has execution permissions |

### Debugging MCP Servers

1. Open the **Output** panel in VS Code (`Ctrl+Shift+U`)
2. Select **"MCP"** from the dropdown
3. View server startup logs and error messages

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 09: Extensions & MCP](README.md) |
| Previous Lesson | [MCP Explained](mcp-explained.md) |
| Next Lesson | [Building Custom Extensions](building-extensions.md) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
