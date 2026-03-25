# Claude Code Glossary

**Claude Code Mastery — March 2026**
**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Core Terminology

| Term | Definition |
|------|-----------|
| **Agentic Loop** | The iterative cycle where Claude reads context, decides on an action, executes it via a tool, observes the result, and repeats until the task is complete. |
| **Anthropic** | The AI safety company that builds Claude, the large language model powering Claude Code. |
| **Auto Mode** | A permission mode (`--allowedTools`) that lets Claude execute approved tool categories without prompting for confirmation each time. |
| **CLAUDE.md** | A special Markdown file placed in your repository that provides persistent instructions, project context, and conventions to Claude Code across sessions. |
| **Claude Code** | Anthropic's official agentic CLI tool that brings Claude directly into your terminal for software engineering tasks. |
| **Context Window** | The maximum amount of text (measured in tokens) that Claude can process in a single conversation. Currently up to 200K tokens for Claude Sonnet and Opus. |
| **Extended Thinking** | A capability where Claude performs deeper, step-by-step reasoning before responding, improving accuracy on complex tasks. Enabled with `--thinking`. |
| **Hooks** | User-defined shell commands that run automatically at specific lifecycle points (pre-tool, post-tool, notification) during a Claude Code session. |
| **MCP (Model Context Protocol)** | An open protocol that allows Claude Code to connect to external tools, databases, and services through standardized server interfaces. |
| **Permission Modes** | Security levels controlling which tools Claude can use without confirmation: `default`, `plan`, `bypassPermissions`. |
| **Slash Commands** | Built-in commands prefixed with `/` (e.g., `/clear`, `/compact`, `/cost`) that control Claude Code behavior during a session. |
| **Subagent** | A child Claude instance spawned by the main agent to handle a subtask independently, such as searching files or running tests in parallel. |
| **Tool Use** | The mechanism by which Claude invokes external capabilities like file reading, writing, bash commands, or MCP servers. |

## Advanced Concepts

| Term | Definition |
|------|-----------|
| **Adaptive Reasoning** | Claude's ability to dynamically adjust its reasoning depth based on task complexity, conserving tokens on simple tasks. |
| **Agent SDK** | Anthropic's Python SDK for building custom agentic applications on top of Claude, supporting multi-agent orchestration. |
| **Allowlist** | A configured list of tools or commands that Claude may execute without user approval in auto mode. |
| **API Key** | A secret credential used to authenticate with the Anthropic API. Set via `ANTHROPIC_API_KEY` environment variable. |
| **Caching (Prompt Caching)** | A technique where previously sent context is cached server-side to reduce latency and cost on subsequent requests. |
| **Compact Mode** | Triggered by `/compact` or automatically when context grows large; summarizes conversation history to free up context window space. |
| **Cost Tracking** | Built-in feature (`/cost`) that displays cumulative token usage and estimated dollar cost for the current session. |
| **Diff View** | The display format Claude uses to show proposed file changes, allowing you to review before accepting. |
| **Headless Mode** | Running Claude Code non-interactively via `claude -p "prompt"`, suitable for CI/CD pipelines and scripts. |
| **Init Command** | `claude /init` generates an initial CLAUDE.md file by analyzing your project structure, dependencies, and conventions. |
| **Max Turns** | In headless mode, the `--max-turns` flag limits how many agentic loop iterations Claude will perform before stopping. |
| **Memory Files** | CLAUDE.md files at various scopes (global `~/.claude/CLAUDE.md`, project root, subdirectories) that persist instructions across sessions. |
| **Multi-root Workspace** | A VS Code or JetBrains setup where Claude Code operates across multiple project folders simultaneously. |
| **OAuth / SSO** | Enterprise authentication methods supported by Claude Code for team deployments, bypassing individual API keys. |
| **Prompt Engineering** | The practice of crafting clear, specific instructions to get optimal results from Claude Code. |
| **Session** | A single continuous conversation with Claude Code, from start to `/clear` or exit. Context accumulates within a session. |
| **Skills** | Reusable slash-command workflows defined in CLAUDE.md or plugins that encapsulate multi-step procedures. |
| **Token** | The basic unit of text processing for LLMs. Roughly 4 characters or 0.75 words in English. Both input and output tokens count toward usage. |
| **Worktree** | A Git feature allowing multiple working directories from a single repository. Claude Code can use worktrees for parallel branch work. |

## MCP-Specific Terms

| Term | Definition |
|------|-----------|
| **MCP Server** | A process that exposes tools, resources, or prompts to Claude Code via the Model Context Protocol. |
| **MCP Transport** | The communication layer (stdio or SSE) used between Claude Code and an MCP server. |
| **Resource (MCP)** | A read-only data source (file, API endpoint, database query) exposed by an MCP server for Claude to reference. |
| **Tool (MCP)** | An executable action exposed by an MCP server that Claude can invoke, such as querying a database or calling an API. |

## Slash Command Reference

| Command | Purpose |
|---------|---------|
| `/clear` | Resets the conversation context and starts fresh |
| `/compact` | Summarizes conversation history to free context window space |
| `/cost` | Displays cumulative token usage and estimated dollar cost |
| `/init` | Generates a CLAUDE.md file by analyzing your project |
| `/help` | Shows available commands and usage information |
| `/model` | Switches the active model mid-session |
| `/review` | Triggers a code review of recent changes |

## Environment Variables

| Variable | Purpose |
|----------|---------|
| `ANTHROPIC_API_KEY` | Authenticates requests to the Anthropic API |
| `CLAUDE_CODE_USE_BEDROCK` | Routes requests through AWS Bedrock instead of direct API |
| `CLAUDE_CODE_USE_VERTEX` | Routes requests through Google Vertex AI |
| `CLAUDE_MODEL` | Overrides the default model (e.g., `claude-sonnet-4-20250514`) |
| `CLAUDE_CODE_MAX_OUTPUT_TOKENS` | Sets maximum response length per turn |
| `CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC` | Disables telemetry and update checks |
| `CLAUDE_CODE_SKIP_CLAUDE_MD` | Skips loading CLAUDE.md files (for debugging) |

---

> **Tip:** Use `/cost` during any session to see real-time token and cost metrics.
