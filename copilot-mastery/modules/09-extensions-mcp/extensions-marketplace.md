# Copilot Extensions Marketplace

**Module 09, Lesson 1 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Copilot Extensions are **third-party integrations** that add new capabilities to Copilot Chat. They appear as chat participants (like `@docker`, `@sentry`, `@azure`) and allow you to interact with external services directly from your development environment.

---

## What Are Copilot Extensions?

Extensions are plugins that:
- Add new `@participant` names to Copilot Chat
- Connect to third-party services and APIs
- Process your queries and return contextualized responses
- Can access external data sources on your behalf

```
┌────────────────────────────────────────────┐
│           Copilot Chat                      │
│                                             │
│   Built-in:        Extensions:              │
│   @workspace        @docker                 │
│   @terminal         @sentry                 │
│   @vscode           @azure                  │
│   @github           @mongodb                │
│                     @linear                  │
│                     @datadog                 │
│                     @hashicorp               │
│                     @stripe                  │
│                     ...and more             │
└────────────────────────────────────────────┘
```

---

## Finding and Installing Extensions

### On GitHub Marketplace

1. Visit [github.com/marketplace?type=apps&copilot_app=true](https://github.com/marketplace)
2. Filter by **"Copilot Extensions"**
3. Browse available extensions
4. Click **Install** on the extension you want
5. Authorize the required permissions
6. The extension becomes available in Copilot Chat

### In VS Code

1. Open Copilot Chat
2. Type `@` to see all available participants
3. Extensions you have installed appear alongside built-in participants

---

## Popular Copilot Extensions (March 2026)

| Extension | What It Does | Example Usage |
|-----------|-------------|---------------|
| **@docker** | Docker container management, Dockerfile help | `@docker How do I optimize this Dockerfile?` |
| **@sentry** | Error tracking and debugging | `@sentry Show me the top errors in production` |
| **@azure** | Azure cloud resource management | `@azure Deploy this app to Azure App Service` |
| **@mongodb** | MongoDB query help and schema design | `@mongodb Create an index for the users collection` |
| **@linear** | Issue tracking and project management | `@linear What issues are assigned to me this sprint?` |
| **@datadog** | Monitoring and observability | `@datadog Show me the latency metrics for /api/users` |
| **@hashicorp** | Terraform and infrastructure as code | `@hashicorp Write a Terraform config for an S3 bucket` |
| **@stripe** | Payment integration help | `@stripe How do I implement subscription billing?` |
| **@vercel** | Deployment and hosting | `@vercel Deploy my Next.js app` |
| **@supabase** | Database and auth management | `@supabase Create a new table for blog posts` |

---

## Extension Permissions

When you install an extension, it requests specific permissions:

| Permission | Description |
|-----------|-------------|
| **Read chat messages** | The extension can see your chat queries |
| **Repository access** | The extension can read your repository files |
| **API access** | The extension connects to its external service |
| **Write access** | Some extensions can modify files or settings |

> **Security Tip:** Only install extensions from trusted publishers. Review permissions carefully before authorizing.

---

## Using Extensions in Chat

Extensions work just like built-in participants:

```
# Ask Docker for help
@docker Create a multi-stage Dockerfile for a Node.js app with TypeScript

# Query Sentry for errors
@sentry What are the most frequent unhandled exceptions this week?

# Manage Azure resources
@azure List all my running App Services and their resource usage

# Get project status from Linear
@linear Show me the burndown chart for the current sprint
```

---

## Extension Types

### Skill-Based Extensions
Provide specific capabilities — generate code, answer questions, perform actions.

### Agent-Based Extensions
Can perform multi-step tasks autonomously, similar to agent mode but with external service access.

### Data Extensions
Provide access to external data sources that Copilot can use as context.

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 09: Extensions & MCP](README.md) |
| Next Lesson | [MCP Explained](mcp-explained.md) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
