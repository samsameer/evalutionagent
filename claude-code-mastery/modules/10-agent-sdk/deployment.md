# Deployment & Production

**Module 10, Lesson 4 — Claude Code Mastery**

**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Overview

Building an agent locally is only half the work. This lesson covers everything required to run Claude Code agents reliably in production: containerization, GitHub Actions integration, monitoring, cost management at scale, and security hardening.

---

## Running Agents in Production

| Concern | Local Development | Production |
|---------|-------------------|------------|
| **Reliability** | Restart manually | Automatic retries and health checks |
| **Observability** | Console logs | Structured logging and alerting |
| **Cost** | Iterate freely | Enforce budgets and rate limits |
| **Security** | API key in `.env` | Secrets manager, least-privilege |

---

## Containerization

```dockerfile
FROM node:20-slim
WORKDIR /app
RUN npm install -g @anthropic-ai/claude-code
COPY package*.json ./
RUN npm ci --production
COPY . .
RUN useradd -m agent && chown -R agent:agent /app
USER agent
CMD ["node", "dist/agent.js"]
```

```bash
docker build -t code-review-agent .
docker run --rm -e ANTHROPIC_API_KEY="$ANTHROPIC_API_KEY" -v /repo:/workspace:ro code-review-agent
```

| Best Practice | Reason |
|--------------|--------|
| `node:20-slim` base | Smaller image, fewer vulnerabilities |
| Non-root user | Limits blast radius if compromised |
| Read-only mounts | Prevents accidental writes |

---

## GitHub Actions Integration

```yaml
# .github/workflows/agent-review.yml
name: Agent Code Review
on:
  pull_request:
    types: [opened, synchronize]
jobs:
  review:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      pull-requests: write
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: "20"
      - name: Run code review agent
        env:
          ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
        run: npm ci && node dist/review-agent.js
```

---

## Monitoring and Logging

```typescript
async function monitoredAgentCall(agent: ClaudeCode, prompt: string) {
  const startTime = Date.now();
  try {
    const response = await agent.sendMessage(prompt);
    logger.info("agent_complete", {
      duration: Date.now() - startTime,
      tokensUsed: response.usage.total_tokens,
    });
    return response;
  } catch (error) {
    logger.error("agent_failed", { error: error.message });
    throw error;
  }
}
```

| Metric | Purpose | Alert Threshold |
|--------|---------|-----------------|
| `agent_request_duration` | Detect slow or stuck agents | > 120 seconds |
| `tokens_per_request` | Track token consumption | > 50,000 per call |
| `error_rate` | Identify systemic failures | > 5% of requests |
| `daily_cost` | Budget enforcement | Approaching spend limit |

---

## Cost Management at Scale

| Strategy | Implementation | Savings |
|----------|---------------|---------|
| Per-agent token limits | `maxTokens: 4096` | Prevents runaway responses |
| Smaller models for simple tasks | `model: "claude-haiku-4-20250514"` | 10-20x cheaper |
| Cache repeated analyses | Key by file hash | Avoids redundant API calls |
| Daily spend caps | Hard limit with cost tracker | Prevents budget overruns |

```typescript
class CostManager {
  private dailySpend = 0;
  constructor(private readonly dailyLimit: number) {}
  async execute(agent: ClaudeCode, prompt: string) {
    if (this.dailySpend >= this.dailyLimit) throw new Error("Daily limit reached");
    const response = await agent.sendMessage(prompt);
    this.dailySpend += response.usage.total_tokens * 0.000003;
    return response;
  }
}
```

---

## Security Considerations

| Risk | Mitigation |
|------|-----------|
| API key exposure | Use secrets managers (AWS Secrets Manager, Vault), never hardcode |
| Malicious code execution | Restrict `bash` tool, use read-only mounts, sandbox containers |
| Prompt injection via code | Validate agent output before acting on it |
| Unbounded resource usage | Set timeouts, token limits, and daily cost caps |
| Data leakage | Scope file access, avoid sending unnecessary code to agents |

```json
{
  "permissions": {
    "allow": ["Bash(npm test)", "Bash(npm run lint)"],
    "deny": ["Bash(rm -rf *)", "Bash(curl *)", "Bash(wget *)"]
  }
}
```

---

## Production Checklist

| Item | Priority |
|------|----------|
| API keys in secrets manager | Required |
| Non-root container user | Required |
| Timeouts on all agent calls | Required |
| Daily cost caps | Required |
| Structured logging | Required |
| Error alerting | Recommended |
| Output validation | Recommended |
| Read-only mounts for reviewers | Recommended |

---

## Navigation

| Direction | Link |
|-----------|------|
| Previous | [Lesson 3: Multi-Agent Patterns](multi-agent-patterns.md) |
| Next | [Module 11: Cheat Sheets](../11-cheat-sheets/) |
| Module Home | [Module 10: Agent SDK](README.md) |
