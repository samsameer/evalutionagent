# Agent SDK Overview

**Module 10, Lesson 1 — Claude Code Mastery**

**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Overview

The Claude Agent SDK provides programmatic access to Claude Code capabilities, allowing you to build custom agents that read, write, and reason about code from your own applications. Available for TypeScript/JavaScript, the SDK lets you move beyond the interactive CLI into fully automated workflows such as CI/CD bots, code review automation, and custom developer tooling.

---

## What Is the Claude Agent SDK?

| Aspect | Detail |
|--------|--------|
| **Package Name** | `@anthropic-ai/claude-code-sdk` (npm) |
| **Language Support** | TypeScript / JavaScript (primary), Python wrapper available |
| **Runtime** | Node.js 18+ |
| **Authentication** | Anthropic API key or Claude Pro/Max plan credentials |
| **Core Capability** | Programmatic access to Claude Code's agentic coding loop |

The SDK wraps the same engine that powers the Claude Code CLI. Your agents get access to file reading, editing, bash execution, search, and all other tools available in interactive mode.

---

## Use Cases

| Use Case | Description |
|----------|-------------|
| **CI/CD Bots** | Automatically review pull requests, suggest fixes, and enforce standards |
| **Code Review Automation** | Agents that analyze diffs, check for bugs, and leave review comments |
| **Custom Developer Tools** | Internal CLIs and dashboards powered by Claude's reasoning |
| **Automated Refactoring** | Batch refactoring across large codebases with agent supervision |
| **Test Generation** | Agents that read source files and generate comprehensive test suites |

---

## Installation

```bash
# Install the SDK via npm
npm install @anthropic-ai/claude-code-sdk

# Or with yarn
yarn add @anthropic-ai/claude-code-sdk

# Python wrapper
pip install claude-code-sdk
```

---

## Authentication Setup

```bash
# Set your API key as an environment variable
export ANTHROPIC_API_KEY="sk-ant-your-key-here"
```

```typescript
import { ClaudeCode } from "@anthropic-ai/claude-code-sdk";

// Authentication via environment variable (recommended)
const agent = new ClaudeCode();

// Or pass the key explicitly
const agent = new ClaudeCode({
  apiKey: process.env.ANTHROPIC_API_KEY,
});
```

---

## Basic Usage

```typescript
import { ClaudeCode } from "@anthropic-ai/claude-code-sdk";

async function main() {
  const agent = new ClaudeCode();

  const response = await agent.sendMessage(
    "Read the file src/index.ts and summarize what it does."
  );

  console.log(response.text);
  console.log(`Tokens used: ${response.usage.total_tokens}`);
}

main().catch(console.error);
```

---

## SDK Architecture

| Component | Role |
|-----------|------|
| **ClaudeCode Client** | Main entry point; manages sessions, authentication, and configuration |
| **Message Loop** | Drives the agentic loop: prompt, tool use, observation, repeat |
| **Tool Registry** | Controls which tools the agent can access (file read, edit, bash, etc.) |
| **Session State** | Maintains conversation history and working directory context |
| **Cost Tracker** | Reports token usage and estimated cost per interaction |

---

## Configuration Options

```typescript
const agent = new ClaudeCode({
  apiKey: process.env.ANTHROPIC_API_KEY,
  model: "claude-sonnet-4-20250514",
  maxTokens: 16384,
  workingDirectory: "/path/to/project",
  allowedTools: ["read", "edit", "bash", "glob", "grep"],
  systemPrompt: "You are a senior code reviewer.",
  timeout: 120000,
});
```

| Option | Default | Description |
|--------|---------|-------------|
| `model` | `claude-sonnet-4-20250514` | Which Claude model to use |
| `maxTokens` | `16384` | Maximum tokens per response |
| `workingDirectory` | `process.cwd()` | Root directory for file operations |
| `allowedTools` | All tools | Restrict which tools the agent can invoke |
| `systemPrompt` | Default | Custom instructions for the agent |
| `timeout` | `120000` | Milliseconds before a turn times out |

---

## Navigation

| Direction | Link |
|-----------|------|
| Previous | [Module 10 Overview](README.md) |
| Next | [Lesson 2: Building Custom Agents](building-agents.md) |
| Module Home | [Module 10: Agent SDK](README.md) |
