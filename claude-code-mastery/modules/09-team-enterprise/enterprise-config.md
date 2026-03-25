# Enterprise Configuration

**Module 09, Lesson 2 — Claude Code Mastery**

**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Overview

Enterprise deployments require centralized control over Claude Code behavior, model access, and security policies. This lesson covers managed policies, SSO and SCIM integration, model restrictions and routing overrides, organization-wide settings, content exclusions, and audit logging for compliance.

---

## Managed Policies

Administrators can enforce organization-wide instructions using managed policy files. These take the highest priority and cannot be overridden by project or user settings.

| Platform | Policy File Location |
|----------|---------------------|
| Linux | `/etc/claude-code/CLAUDE.md` |
| macOS | `/Library/Application Support/claude-code/CLAUDE.md` |
| Windows | `%ProgramData%\claude-code\CLAUDE.md` |

Deploy these files using your existing configuration management tools (Ansible, Chef, Puppet, MDM profiles).

---

## SSO and SCIM Integration

| Feature | Protocol | Purpose |
|---------|----------|---------|
| SSO | SAML 2.0 / OIDC | Authenticate developers via corporate identity provider |
| SCIM | SCIM 2.0 | Automatically provision and deprovision user accounts |
| Directory sync | AD / Okta / Azure AD | Keep Claude Code seats aligned with your directory |

SSO ensures developers authenticate through your identity provider. SCIM automates seat management — when an employee leaves, their Claude Code access is revoked automatically.

---

## Model Restrictions (availableModels)

Restrict which models your organization allows through managed settings:

```json
{
  "availableModels": [
    "claude-sonnet-4-20250514",
    "claude-haiku-35-20241022"
  ]
}
```

| Strategy | Models Allowed | Use Case |
|----------|----------------|----------|
| Cost-conscious | Sonnet + Haiku only | Keep spend predictable |
| Quality-focused | Opus + Sonnet only | Ensure high-quality outputs |
| Single model | Sonnet only | Simplest cost management |
| Full access | All models | Maximum flexibility |

---

## Model Overrides (Bedrock / Vertex Routing)

Organizations using AWS Bedrock or Google Vertex AI can route traffic through their own cloud accounts:

```json
{
  "modelOverrides": {
    "claude-sonnet-4-20250514": {
      "provider": "bedrock",
      "region": "us-east-1",
      "modelId": "anthropic.claude-sonnet-4-20250514-v1:0"
    },
    "claude-haiku-35-20241022": {
      "provider": "vertex",
      "region": "us-central1",
      "modelId": "claude-haiku-35@20241022"
    }
  }
}
```

| Provider | Environment Variables | Benefit |
|----------|-----------------------|---------|
| Bedrock | `ANTHROPIC_MODEL`, `AWS_REGION`, `AWS_PROFILE` | Traffic stays in your AWS account |
| Vertex | `ANTHROPIC_MODEL`, `CLOUD_ML_REGION` | Traffic stays in your GCP project |
| Direct API | `ANTHROPIC_API_KEY` | Simplest setup, billed through Anthropic |

---

## Organization-Wide Settings

```json
{
  "permissions": {
    "deny": [
      "Bash(curl *)",
      "Bash(wget *)",
      "Bash(rm -rf /)",
      "WebFetch(*)"
    ]
  },
  "settings": {
    "autoUpdaterEnabled": false,
    "telemetryEnabled": false
  }
}
```

| Setting Category | Examples | Purpose |
|-----------------|----------|---------|
| Tool denylists | Block network access, destructive commands | Reduce risk surface |
| Auto-update control | Disable auto-updates | Pin to validated versions |
| Telemetry | Disable telemetry | Meet data residency requirements |
| Default model | Set organization default | Standardize cost and quality |

---

## Content Exclusions

Prevent Claude Code from reading sensitive files:

```json
{
  "contentExclusions": [
    "**/*.env",
    "**/*.pem",
    "**/*.key",
    "**/secrets/**",
    "**/credentials/**"
  ]
}
```

Content exclusions ensure that even if a developer asks Claude to read a sensitive file, the request is blocked before any content reaches the API.

---

## Audit Logging

Enterprise plans provide audit logs for compliance and monitoring:

| Log Event | Data Captured | Purpose |
|-----------|---------------|---------|
| Session start | User, timestamp, project | Track usage patterns |
| Model selection | Model ID, user | Monitor cost allocation |
| Tool execution | Command, approval status | Security auditing |
| File access | File paths read/written | Data access compliance |
| Permission changes | Setting modifications | Change management |

---

## Navigation

| Direction | Link |
|-----------|------|
| Previous | [Team Setup & Onboarding](team-setup.md) |
| Next | [Cost Management & Monitoring](cost-management.md) |
| Module Home | [Module 09: Team & Enterprise](README.md) |
