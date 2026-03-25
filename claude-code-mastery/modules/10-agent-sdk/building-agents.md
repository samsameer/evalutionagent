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

Control what the agent can do by restricting its tool set:

```typescript
// Read-only agent: can inspect code but never modify it
const reviewer = new ClaudeCode({
  allowedTools: ["read", "glob", "grep"],
  systemPrompt: "You review code. You cannot modify files.",
});

// Full-access agent: can read, write, and run commands
const developer = new ClaudeCode({
  allowedTools: ["read", "edit", "write", "bash", "glob", "grep"],
  systemPrompt: "You are a senior developer. Implement requested changes.",
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

System prompts define the agent's persona, rules, and output format:

```typescript
const codeReviewer = new ClaudeCode({
  systemPrompt: `You are a senior code reviewer at a fintech company.

Rules:
- Flag any security vulnerabilities immediately
- Check for proper error handling in all async functions
- Verify that database queries use parameterized statements
- Rate each file: PASS, WARN, or FAIL

Output format:
- Start with a summary table of files reviewed
- Then provide detailed findings per file
- End with an overall verdict`,
});
```

---

## Handling Conversation Turns

Agents support multi-turn conversations with persistent context:

```typescript
const agent = new ClaudeCode({
  workingDirectory: "/home/user/my-project",
});

// Turn 1: Agent reads and understands the codebase
const turn1 = await agent.sendMessage(
  "Read src/auth.ts and identify any security concerns."
);
console.log("Analysis:", turn1.text);

// Turn 2: Follow up with context from turn 1
const turn2 = await agent.sendMessage(
  "Now fix the issues you identified. Show me the changes."
);
console.log("Fixes:", turn2.text);

// Turn 3: Verify the fixes
const turn3 = await agent.sendMessage(
  "Run the test suite to make sure nothing broke."
);
console.log("Tests:", turn3.text);
```

---

## Error Handling

```typescript
import { ClaudeCode, AgentError, TimeoutError, RateLimitError }
  from "@anthropic-ai/claude-code-sdk";

async function safeAgentCall(agent: ClaudeCode, prompt: string) {
  try {
    const response = await agent.sendMessage(prompt);
    return response;
  } catch (error) {
    if (error instanceof TimeoutError) {
      console.error("Agent timed out. Consider increasing timeout or simplifying the task.");
    } else if (error instanceof RateLimitError) {
      console.error(`Rate limited. Retry after ${error.retryAfter}s`);
      await sleep(error.retryAfter * 1000);
      return agent.sendMessage(prompt);  // Retry once
    } else if (error instanceof AgentError) {
      console.error(`Agent error: ${error.message}`);
    } else {
      throw error;  // Unknown error, propagate
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

async function reviewPullRequest(diffContent: string): Promise<ReviewResult> {
  const agent = new ClaudeCode({
    allowedTools: ["read", "glob", "grep"],
    systemPrompt: `You are a strict code reviewer. Analyze the provided diff.
Return your review as JSON with keys: summary, issues (array), verdict.
verdict must be APPROVE or REQUEST_CHANGES.`,
    maxTokens: 8192,
  });

  const response = await agent.sendMessage(
    `Review this pull request diff:\n\n${diffContent}`
  );

  return JSON.parse(response.text) as ReviewResult;
}

// Usage
const diff = await getDiffFromGitHub(prNumber);
const review = await reviewPullRequest(diff);

console.log(`Verdict: ${review.verdict}`);
console.log(`Issues found: ${review.issues.length}`);
review.issues.forEach((issue, i) => console.log(`  ${i + 1}. ${issue}`));
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
