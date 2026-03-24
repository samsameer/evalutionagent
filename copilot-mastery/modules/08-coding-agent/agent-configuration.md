# Agent Configuration & Permissions

**Module 08, Lesson 4 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

The Copilot Coding Agent runs in a secure, sandboxed environment. This lesson covers how to configure its permissions, define what tools it can use, and set up the development environment it operates in.

---

## The copilot-setup-steps.yml File

The coding agent uses a configuration file to set up its development environment. Create this file at `.github/copilot-setup-steps.yml`:

```yaml
# .github/copilot-setup-steps.yml
steps:
  - name: Install dependencies
    run: npm install

  - name: Build the project
    run: npm run build

  - name: Run database migrations
    run: npx prisma migrate deploy
    env:
      DATABASE_URL: ${{ secrets.DATABASE_URL }}
```

This tells the agent how to set up the project before it starts coding.

---

## Environment Configuration

### Node.js / JavaScript Project

```yaml
steps:
  - name: Setup Node.js
    uses: actions/setup-node@v4
    with:
      node-version: '20'

  - name: Install dependencies
    run: npm ci

  - name: Verify build
    run: npm run build
```

### Python Project

```yaml
steps:
  - name: Setup Python
    uses: actions/setup-python@v5
    with:
      python-version: '3.12'

  - name: Install dependencies
    run: pip install -r requirements.txt

  - name: Run migrations
    run: python manage.py migrate
```

### Go Project

```yaml
steps:
  - name: Setup Go
    uses: actions/setup-go@v5
    with:
      go-version: '1.22'

  - name: Install dependencies
    run: go mod download
```

---

## Security Permissions

### Network Firewall

The coding agent runs in a **sandboxed environment** with restricted network access. By default:

- **Allowed:** Package registries (npm, PyPI, Maven, etc.)
- **Allowed:** GitHub API access
- **Blocked:** Arbitrary internet access
- **Blocked:** Internal/private network access

### Configuring Allowed Domains

For projects that need additional network access during setup:

```yaml
# In repository settings or copilot-setup-steps.yml
network:
  allowed-domains:
    - "registry.npmjs.org"
    - "pypi.org"
    - "api.example.com"  # Your API for integration tests
```

---

## Secrets and Environment Variables

The coding agent can access **repository secrets** for setup steps:

```yaml
steps:
  - name: Setup environment
    run: |
      echo "Setting up test database"
      npm run db:setup
    env:
      DATABASE_URL: ${{ secrets.TEST_DATABASE_URL }}
      API_KEY: ${{ secrets.TEST_API_KEY }}
```

> **Important:** Only provide secrets necessary for **testing and building**. Never provide production credentials to the coding agent.

---

## What the Agent Can and Cannot Do

| Can Do | Cannot Do |
|--------|-----------|
| Read all files in the repository | Access production databases |
| Create/modify/delete files | Deploy to production |
| Run build and test commands | Access private networks |
| Install dependencies | Use arbitrary internet services |
| Create branches | Push to protected branches |
| Open pull requests | Merge PRs (you must review) |
| Respond to review comments | Access other repositories |

---

## Best Practices

1. **Keep setup steps simple** — Complex setup increases failure risk
2. **Use test databases** — Never connect to production
3. **Pin dependency versions** — Ensure reproducible builds
4. **Set reasonable timeouts** — Agent sessions have time limits
5. **Review the session log** — Check if the agent struggled with setup

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 08: Coding Agent](README.md) |
| Previous Lesson | [Reviewing Agent PRs](reviewing-agent-prs.md) |
| Next Module | [Module 09: Extensions & MCP](../09-extensions-mcp/) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
