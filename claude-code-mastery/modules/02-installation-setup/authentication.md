# Authentication & Login

**Module 02, Lesson 3 — Claude Code Mastery**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Claude Code supports multiple authentication methods. This lesson covers OAuth login, API keys, enterprise SSO, and cloud provider authentication.

---

## Method 1: OAuth Login (Recommended)

This is the default for Claude Pro, Max, Team, and Enterprise users.

### Step 1: Launch Claude Code

```bash
claude
```

### Step 2: Authenticate

A browser window opens automatically. If it doesn't, press `c` to copy the login URL.

### Step 3: Sign In

Sign in with your Claude.ai account (the same one you use for claude.ai).

### Step 4: Authorize

Grant Claude Code access to your account. You'll be redirected back to the terminal.

### Step 5: Verify

Claude Code will show a welcome message. You're ready to go.

---

## Method 2: API Key

For API pay-as-you-go users or custom setups.

### Option A: Environment Variable

```bash
export ANTHROPIC_API_KEY=sk-ant-api03-xxxxxxxxxxxxx
claude
```

Add to your shell profile for persistence:

```bash
echo 'export ANTHROPIC_API_KEY=sk-ant-api03-xxxxxxxxxxxxx' >> ~/.bashrc
source ~/.bashrc
```

### Option B: At Startup

```bash
ANTHROPIC_API_KEY=sk-ant-xxxxx claude
```

---

## Method 3: Dynamic Credentials (Enterprise)

For rotating or short-lived tokens, use the `apiKeyHelper` setting:

```json
{
  "apiKeyHelper": "/path/to/credential-script.sh"
}
```

The script should output the API key to stdout:

```bash
#!/bin/bash
# Example: fetch from a secrets manager
aws secretsmanager get-secret-value \
  --secret-id anthropic-api-key \
  --query SecretString --output text
```

The key is refreshed every 5 minutes or on HTTP 401. Configure the refresh interval:

```bash
export CLAUDE_CODE_API_KEY_HELPER_TTL_MS=300000  # 5 minutes
```

---

## Method 4: Cloud Provider Authentication

### Amazon Bedrock

```bash
export CLAUDE_CODE_USE_BEDROCK=1
export AWS_REGION=us-east-1
export AWS_ACCESS_KEY_ID=your-key
export AWS_SECRET_ACCESS_KEY=your-secret
claude
```

### Google Vertex AI

```bash
export CLAUDE_CODE_USE_VERTEX=1
export CLOUD_ML_REGION=us-east5
export ANTHROPIC_VERTEX_PROJECT_ID=your-project-id
claude
```

### Microsoft Foundry

```bash
export CLAUDE_CODE_USE_FOUNDRY=1
claude
```

---

## Authentication Precedence

When multiple credentials are available, Claude Code uses this priority:

1. Cloud provider env vars (Bedrock, Vertex, Foundry)
2. `ANTHROPIC_AUTH_TOKEN` (bearer token for API gateways)
3. `ANTHROPIC_API_KEY` (direct API key)
4. `apiKeyHelper` script
5. OAuth from `/login` (default for subscriptions)

---

## Credential Storage

| Platform | Storage Location |
|----------|-----------------|
| macOS | Encrypted Keychain |
| Linux | `~/.claude/.credentials.json` (mode 0600) |
| Windows (WSL) | `~/.claude/.credentials.json` (mode 0600) |

Override the config directory:

```bash
export CLAUDE_CONFIG_DIR=/custom/path
```

---

## Logout and Re-authenticate

```bash
# Inside Claude Code:
/logout

# Then re-authenticate:
/login
```

---

## Verify Authentication

```bash
# Inside Claude Code:
/doctor
```

The doctor command checks your authentication status and reports any issues.

---

**Next:** [Terminal Setup & Configuration](terminal-setup.md)

[← Back to Module Overview](README.md)

---

*Module 02, Lesson 3 — Claude Code Mastery — March 2026*
