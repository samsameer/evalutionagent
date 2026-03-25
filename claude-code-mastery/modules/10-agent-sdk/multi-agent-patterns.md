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

One central agent receives the task, breaks it down, and delegates to specialized sub-agents:

```typescript
async function orchestrator(task: string) {
  const planner = new ClaudeCode({
    allowedTools: ["read", "glob"],
    systemPrompt: `Break tasks into subtasks. Return JSON:
{ subtasks: [{ type: "review"|"implement"|"test", description: string }] }`,
  });
  const { subtasks } = JSON.parse((await planner.sendMessage(task)).text);

  const specialists: Record<string, ClaudeCode> = {
    review: new ClaudeCode({ allowedTools: ["read", "glob", "grep"] }),
    implement: new ClaudeCode({ allowedTools: ["read", "edit", "write", "bash"] }),
    test: new ClaudeCode({ allowedTools: ["read", "write", "bash"] }),
  };

  return Promise.all(subtasks.map(async (s) => ({
    type: s.type,
    output: (await specialists[s.type].sendMessage(s.description)).text,
  })));
}
```

---

## Pipeline Pattern

Each agent processes the output of the previous one, like an assembly line:

```typescript
async function pipeline(sourceFile: string) {
  const analyzer = new ClaudeCode({ allowedTools: ["read", "grep", "glob"] });
  const analysis = await analyzer.sendMessage(`Analyze ${sourceFile} for issues.`);

  const fixer = new ClaudeCode({ allowedTools: ["read", "edit"] });
  await fixer.sendMessage(`Fix these issues in ${sourceFile}:\n${analysis.text}`);

  const verifier = new ClaudeCode({ allowedTools: ["read", "bash"] });
  return await verifier.sendMessage(`Run npm test to verify fixes in ${sourceFile}.`);
}
```

---

## Team Pattern

Multiple agents work on independent subtasks in parallel and results are merged:

```typescript
async function teamReview(files: string[]) {
  const createReviewer = (focus: string) => new ClaudeCode({
    allowedTools: ["read", "grep", "glob"],
    systemPrompt: `Review code for ${focus} issues only. Return JSON findings.`,
  });

  const fileList = files.join(", ");
  const [security, performance, style] = await Promise.all([
    createReviewer("security").sendMessage(`Review: ${fileList}`),
    createReviewer("performance").sendMessage(`Review: ${fileList}`),
    createReviewer("code style").sendMessage(`Review: ${fileList}`),
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

One agent does the work; another reviews and requests corrections if needed:

```typescript
async function supervisedTask(task: string, maxIterations = 3) {
  const worker = new ClaudeCode({ allowedTools: ["read", "edit", "write", "bash"] });
  const supervisor = new ClaudeCode({
    allowedTools: ["read", "glob", "grep"],
    systemPrompt: `Review work. Return JSON: { approved: boolean, feedback: string }`,
  });
  let output = await worker.sendMessage(task);
  for (let i = 0; i < maxIterations; i++) {
    const { approved, feedback } = JSON.parse(
      (await supervisor.sendMessage(`Review: ${output.text}`)).text
    );
    if (approved) return { result: output.text, iterations: i + 1 };
    output = await worker.sendMessage(`Fix these issues:\n${feedback}`);
  }
  throw new Error("Max iterations reached without approval");
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

| Factor | Mitigation |
|--------|------------|
| Each agent has its own context window | Keep agent scopes narrow |
| Parallel agents run simultaneously | Set per-agent `maxTokens: 4096` and `timeout: 60000` |
| Supervisor loops can repeat | Cap iteration count (e.g., `maxIterations = 3`) |
| Orchestrator planning overhead | Cache plans for similar tasks |

---

## Navigation

| Direction | Link |
|-----------|------|
| Previous | [Lesson 2: Building Custom Agents](building-agents.md) |
| Next | [Lesson 4: Deployment & Production](deployment.md) |
| Module Home | [Module 10: Agent SDK](README.md) |
