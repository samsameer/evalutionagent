# Multi-Agent Patterns

**Module 10, Lesson 3 — Claude Code Mastery**

**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Overview

Single agents are powerful, but complex tasks often require multiple agents working together. This lesson covers four proven multi-agent patterns: orchestrator, pipeline, team, and supervisor. You will learn when to use each pattern, how to implement them, and how to manage the cost implications of running multiple agents.

---

## Pattern Summary

| Pattern | Structure | Best For | Cost |
|---------|-----------|----------|------|
| **Orchestrator** | One agent delegates to specialists | Complex tasks needing diverse expertise | Medium-High |
| **Pipeline** | Agents process sequentially | Multi-stage workflows with clear handoffs | Medium |
| **Team** | Agents work in parallel | Independent subtasks that can run concurrently | High (parallel) |
| **Supervisor** | One agent reviews others' output | Quality-critical workflows needing verification | High |

---

## Orchestrator Pattern

One central agent receives the task, breaks it down, and delegates to specialized sub-agents.

```typescript
import { ClaudeCode } from "@anthropic-ai/claude-code-sdk";

async function orchestrator(task: string) {
  const planner = new ClaudeCode({
    allowedTools: ["read", "glob"],
    systemPrompt: `You are a project planner. Break tasks into subtasks.
Return JSON: { subtasks: [{ type: "review"|"implement"|"test", description: string }] }`,
  });

  const plan = await planner.sendMessage(task);
  const { subtasks } = JSON.parse(plan.text);

  const specialists: Record<string, ClaudeCode> = {
    review: new ClaudeCode({
      allowedTools: ["read", "glob", "grep"],
      systemPrompt: "You are a code reviewer. Analyze code for issues.",
    }),
    implement: new ClaudeCode({
      allowedTools: ["read", "edit", "write", "bash"],
      systemPrompt: "You are a developer. Implement the requested changes.",
    }),
    test: new ClaudeCode({
      allowedTools: ["read", "write", "bash"],
      systemPrompt: "You are a QA engineer. Write and run tests.",
    }),
  };

  const results = [];
  for (const subtask of subtasks) {
    const agent = specialists[subtask.type];
    const result = await agent.sendMessage(subtask.description);
    results.push({ type: subtask.type, output: result.text });
  }

  return results;
}
```

---

## Pipeline Pattern

Each agent processes the output of the previous one, like an assembly line.

```typescript
async function pipeline(sourceFile: string) {
  // Stage 1: Analyze
  const analyzer = new ClaudeCode({
    allowedTools: ["read", "grep", "glob"],
    systemPrompt: "Analyze code and list all issues as JSON array.",
  });
  const analysis = await analyzer.sendMessage(`Analyze ${sourceFile}`);

  // Stage 2: Fix
  const fixer = new ClaudeCode({
    allowedTools: ["read", "edit"],
    systemPrompt: "Fix the issues described. Edit files directly.",
  });
  await fixer.sendMessage(
    `Fix these issues in ${sourceFile}:\n${analysis.text}`
  );

  // Stage 3: Verify
  const verifier = new ClaudeCode({
    allowedTools: ["read", "bash"],
    systemPrompt: "Run tests and confirm all issues are resolved.",
  });
  const verification = await verifier.sendMessage(
    `Verify fixes in ${sourceFile}. Run: npm test`
  );

  return verification.text;
}
```

| Stage | Agent Role | Tools | Input | Output |
|-------|-----------|-------|-------|--------|
| 1 | Analyzer | read, grep, glob | Source file path | List of issues (JSON) |
| 2 | Fixer | read, edit | Issues + file path | Modified files |
| 3 | Verifier | read, bash | File path | Test results |

---

## Team Pattern

Multiple agents work on independent subtasks in parallel, and results are merged.

```typescript
async function teamReview(files: string[]) {
  const createReviewer = (focus: string) => new ClaudeCode({
    allowedTools: ["read", "grep", "glob"],
    systemPrompt: `You review code for ${focus} issues only. Return JSON findings.`,
  });

  const reviewers = {
    security: createReviewer("security"),
    performance: createReviewer("performance"),
    style: createReviewer("code style and readability"),
  };

  const fileList = files.join(", ");

  // Run all reviewers in parallel
  const [security, performance, style] = await Promise.all([
    reviewers.security.sendMessage(`Review these files: ${fileList}`),
    reviewers.performance.sendMessage(`Review these files: ${fileList}`),
    reviewers.style.sendMessage(`Review these files: ${fileList}`),
  ]);

  return {
    security: JSON.parse(security.text),
    performance: JSON.parse(performance.text),
    style: JSON.parse(style.text),
  };
}
```

---

## Supervisor Pattern

One agent does the work; another reviews it and requests corrections if needed.

```typescript
async function supervisedTask(task: string, maxIterations = 3) {
  const worker = new ClaudeCode({
    allowedTools: ["read", "edit", "write", "bash"],
    systemPrompt: "You are a developer. Implement the requested changes.",
  });

  const supervisor = new ClaudeCode({
    allowedTools: ["read", "glob", "grep"],
    systemPrompt: `You are a senior engineer reviewing work.
Return JSON: { approved: boolean, feedback: string }`,
  });

  let workerOutput = await worker.sendMessage(task);

  for (let i = 0; i < maxIterations; i++) {
    const review = await supervisor.sendMessage(
      `Review the changes just made for this task: "${task}"\n\nWorker output:\n${workerOutput.text}`
    );

    const { approved, feedback } = JSON.parse(review.text);

    if (approved) {
      return { result: workerOutput.text, iterations: i + 1 };
    }

    workerOutput = await worker.sendMessage(
      `The reviewer found issues:\n${feedback}\n\nPlease fix them.`
    );
  }

  throw new Error("Max review iterations reached without approval");
}
```

---

## When to Use Each Pattern

| Scenario | Recommended Pattern | Reason |
|----------|-------------------|--------|
| Feature implementation with review | Supervisor | Quality gate before merging |
| Analyzing a PR from multiple angles | Team | Independent concerns, parallel execution |
| Migrating a codebase step by step | Pipeline | Clear sequential stages |
| Complex project with mixed tasks | Orchestrator | Central coordination of diverse work |
| Simple single-purpose automation | None (single agent) | Multi-agent overhead not justified |

---

## Cost Considerations

| Factor | Impact | Mitigation |
|--------|--------|------------|
| Each agent has its own context window | Multiplied token usage | Keep agent scopes narrow |
| Parallel agents run simultaneously | Burst API costs | Set per-agent token limits |
| Supervisor loops can repeat | Unbounded cost risk | Cap iteration count |
| Orchestrator planning step | Overhead per task | Cache plans for similar tasks |

```typescript
// Set per-agent cost limits
const agent = new ClaudeCode({
  maxTokens: 4096,       // Limit output tokens per turn
  timeout: 60000,        // Kill after 60 seconds
});
```

---

## Navigation

| Direction | Link |
|-----------|------|
| Previous | [Lesson 2: Building Custom Agents](building-agents.md) |
| Next | [Lesson 4: Deployment & Production](deployment.md) |
| Module Home | [Module 10: Agent SDK](README.md) |
