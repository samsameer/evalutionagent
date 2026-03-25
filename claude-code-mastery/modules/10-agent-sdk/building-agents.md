# Building Custom Agents

**Module 10, Lesson 2 — Claude Code Mastery**

**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Overview

This lesson walks through building custom agents with the Claude Agent SDK. You will learn how to create agents, configure their available tools, set system prompts that shape behavior, handle multi-turn conversations, and implement robust error handling. By the end, you will have built a working code review bot.

---

## Creating a Basic Agent

```typescript
import { ClaudeCode } from "@anthropic-ai/claude-code-sdk";

const agent = new ClaudeCode({
  workingDirectory: "/home/user/my-project",
  systemPrompt: "You are a helpful coding assistant.",
});

const response = await agent.sendMessage("What files are in the src/ directory?");
console.log(response.text);
```

---

## Configuring Available Tools

```typescript
// Read-only agent — can inspect code but never modify it
const reviewer = new ClaudeCode({ allowedTools: ["read", "glob", "grep"] });

// Full-access agent — can read, write, and run commands
const developer = new ClaudeCode({
  allowedTools: ["read", "edit", "write", "bash", "glob", "grep"],
});
```

| Tool | Capability | Risk Level |
|------|-----------|------------|
| `read` | Read file contents | Low |
| `glob` | Find files by pattern | Low |
| `grep` | Search file contents | Low |
| `edit` | Modify existing files | Medium |
| `write` | Create new files | Medium |
| `bash` | Execute shell commands | High |

---

## Setting System Prompts

```typescript
const codeReviewer = new ClaudeCode({
  systemPrompt: `You are a senior code reviewer at a fintech company.
Rules:
- Flag security vulnerabilities immediately
- Check for proper error handling in async functions
- Rate each file: PASS, WARN, or FAIL`,
});
```

---

## Handling Conversation Turns

```typescript
const agent = new ClaudeCode({ workingDirectory: "/home/user/my-project" });
const turn1 = await agent.sendMessage("Read src/auth.ts and identify security concerns.");
const turn2 = await agent.sendMessage("Now fix the issues you identified.");
const turn3 = await agent.sendMessage("Run the test suite to make sure nothing broke.");
```

---

## Error Handling

```typescript
import { ClaudeCode, TimeoutError, RateLimitError } from "@anthropic-ai/claude-code-sdk";

async function safeAgentCall(agent: ClaudeCode, prompt: string) {
  try {
    return await agent.sendMessage(prompt);
  } catch (error) {
    if (error instanceof TimeoutError) {
      console.error("Agent timed out. Simplify the task or increase timeout.");
    } else if (error instanceof RateLimitError) {
      await new Promise((r) => setTimeout(r, error.retryAfter * 1000));
      return agent.sendMessage(prompt);
    } else {
      throw error;
    }
  }
}
```

| Error Type | Cause | Recovery Strategy |
|-----------|-------|-------------------|
| `TimeoutError` | Agent took too long | Increase timeout or break into smaller tasks |
| `RateLimitError` | Too many API calls | Wait and retry with exponential backoff |
| `AgentError` | Tool failure or invalid state | Log details and retry or escalate |
| `AuthenticationError` | Invalid API key | Check credentials and environment variables |

---

## Example: Code Review Bot

```typescript
import { ClaudeCode } from "@anthropic-ai/claude-code-sdk";

interface ReviewResult {
  summary: string;
  issues: string[];
  verdict: "APPROVE" | "REQUEST_CHANGES";
}

async function reviewPullRequest(diff: string): Promise<ReviewResult> {
  const agent = new ClaudeCode({
    allowedTools: ["read", "glob", "grep"],
    systemPrompt: `Analyze the diff. Return JSON: { summary, issues[], verdict }.`,
  });
  const response = await agent.sendMessage(`Review this diff:\n\n${diff}`);
  return JSON.parse(response.text) as ReviewResult;
}

const review = await reviewPullRequest(await getDiffFromGitHub(prNumber));
console.log(`Verdict: ${review.verdict}, Issues: ${review.issues.length}`);
```

---

## Best Practices

| Practice | Rationale |
|----------|-----------|
| Use the smallest tool set possible | Reduces risk of unintended side effects |
| Set explicit system prompts | Prevents the agent from drifting off-task |
| Implement timeouts on every call | Prevents runaway agents from burning tokens |
| Log all tool invocations | Essential for debugging and auditing |
| Parse structured output with validation | Agents can produce malformed JSON; always validate |
| Test agents with known inputs first | Verify behavior before connecting to real systems |

---

## Navigation

| Direction | Link |
|-----------|------|
| Previous | [Lesson 1: SDK Overview](sdk-overview.md) |
| Next | [Lesson 3: Multi-Agent Patterns](multi-agent-patterns.md) |
| Module Home | [Module 10: Agent SDK](README.md) |
