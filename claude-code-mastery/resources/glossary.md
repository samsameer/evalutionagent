# Claude Code Glossary

**Claude Code Mastery — March 2026**
**Instructor: Jabbir Basha, Principal AI Engineer**

---

A comprehensive glossary of terms used throughout Claude Code and the Anthropic ecosystem.

## Core Concepts

| Term | Definition |
|------|-----------|
| **Agentic Loop** | The iterative cycle where Claude reads context, decides on an action, executes a tool, observes the result, and repeats until the task is complete. |
| **Anthropic** | The AI safety company that builds Claude, the large language model powering Claude Code. |
| **Claude** | Anthropic's family of large language models, including Sonnet, Opus, and Haiku variants. |
| **Claude Code** | Anthropic's official agentic CLI tool that lets developers use Claude directly in their terminal for coding tasks. |
| **CLAUDE.md** | A markdown file placed in a project root (or subdirectories) that provides persistent context, conventions, and instructions to Claude Code across sessions. |
| **Context Window** | The maximum amount of text (measured in tokens) that Claude can process in a single conversation. Larger windows allow more code and history to be considered. |
| **Token** | The fundamental unit of text processing. Roughly 4 characters or 0.75 words in English. Used to measure input size, output size, and cost. |

## Features & Capabilities

| Term | Definition |
|------|-----------|
| **Adaptive Reasoning** | Claude's ability to dynamically adjust the depth and approach of its reasoning based on task complexity, using more thinking budget for harder problems. |
| **Auto Mode** | A permission mode where Claude Code automatically approves safe tool calls (reads, searches) while still prompting for potentially destructive actions (writes, deletes). |
| **Extended Thinking** | A feature that gives Claude a dedicated "thinking" scratchpad to reason through complex problems step by step before responding. Consumes additional tokens. |
| **Hooks** | User-defined shell commands that run automatically before or after specific Claude Code events (e.g., before a file edit, after a command). Used for linting, formatting, and validation. |
| **MCP (Model Context Protocol)** | An open protocol that allows Claude Code to connect to external tools and data sources through a standardized server interface. |
| **Permission Modes** | Configuration settings that control which actions Claude Code can perform without asking — ranges from fully interactive to fully autonomous. |
| **Prompt Caching** | A cost-optimization feature where Anthropic caches repeated prompt prefixes, reducing token charges for conversations that share common context like CLAUDE.md. |
| **Slash Commands** | Built-in commands prefixed with `/` that control Claude Code behavior, such as `/clear`, `/compact`, `/config`, `/help`, and `/review`. |
| **Skills** | Reusable prompt snippets stored as markdown files that can be invoked as slash commands, allowing teams to codify common workflows. |
| **Subagent** | A child instance of Claude spawned by the main agent to handle a subtask independently, allowing parallel work on complex problems. |
| **Tool Use** | Claude's ability to invoke external tools (file read/write, bash commands, search) to interact with the development environment. |

## Architecture & Modes

| Term | Definition |
|------|-----------|
| **Allowlist** | A list of specific tools or commands that Claude Code is pre-approved to run without prompting the user. Configured in settings or CLAUDE.md. |
| **Compact Mode** | A conversation management feature that summarizes older context to free up space in the context window for new information. |
| **Conversation History** | The full sequence of messages, tool calls, and results in a Claude Code session. Stored locally and resumable. |
| **Headless Mode** | Running Claude Code non-interactively via `claude -p "prompt"`, useful for CI/CD pipelines and automation scripts. |
| **Multi-turn Conversation** | An extended back-and-forth session where Claude retains context from earlier messages to build on previous work. |
| **Worktree** | A Git feature that Claude Code leverages to work on multiple branches simultaneously without switching, enabling parallel development tasks. |

## API & Integration

| Term | Definition |
|------|-----------|
| **Agent SDK** | Anthropic's official SDK for building custom agentic applications on top of Claude, used programmatically rather than via the CLI. |
| **API Key** | A secret credential used to authenticate with Anthropic's API. Required for direct API usage; Claude Code can also authenticate via OAuth. |
| **Max Mode** | Using Claude with Opus-level models for maximum capability on complex tasks, at higher token cost. Toggled with `/model`. |
| **MCP Server** | A process that implements the Model Context Protocol, exposing tools and resources (databases, APIs, file systems) to Claude Code. |
| **MCP Transport** | The communication layer for MCP — either `stdio` (local process) or `sse` (remote HTTP server). |
| **OAuth** | The authentication method used when signing into Claude Code with an Anthropic account, as an alternative to raw API keys. |
| **Streaming** | The real-time delivery of Claude's response token by token, allowing users to see output as it is generated. |

## Cost & Performance

| Term | Definition |
|------|-----------|
| **Input Tokens** | Tokens sent to Claude (your prompt, code, context). Priced lower than output tokens. |
| **Output Tokens** | Tokens generated by Claude (responses, code, explanations). Priced higher than input tokens. |
| **Rate Limiting** | Throttling applied when API usage exceeds plan limits. Results in slower responses or temporary blocks. |
| **Token Budget** | A configurable cap on how many tokens Claude can use for thinking or responding in a single turn. |

---

> **Tip:** Use `/help` inside Claude Code to see built-in documentation for any command or feature.
