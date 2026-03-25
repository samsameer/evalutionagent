# Deployment & Production

**Module 10, Lesson 4 — Claude Code Mastery**

**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Overview

Building an agent locally is only half the work. This lesson covers running Claude Code agents reliably in production: containerization, CI/CD integration, monitoring, cost management, and security.

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
    logger.info("complete", { duration: Date.now() - startTime, tokens: response.usage.total_tokens });
    return response;
  } catch (error) {
    logger.error("failed", { error: error.message });
    throw error;
  }
}
```

| Metric | Alert Threshold |
|--------|-----------------|
| `request_duration` | > 120 seconds |
| `tokens_per_request` | > 50,000 per call |
| `error_rate` | > 5% of requests |
| `daily_cost` | Approaching spend limit |

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
| API key exposure | Use secrets managers (Vault, AWS Secrets Manager) |
| Malicious code execution | Restrict `bash` tool, sandbox containers |
| Prompt injection | Validate agent output before acting on it |
| Unbounded resources | Set timeouts, token limits, daily cost caps |

```json
{
  "permissions": {
    "allow": ["Bash(npm test)", "Bash(npm run lint)"],
    "deny": ["Bash(rm -rf *)", "Bash(curl *)"]
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
