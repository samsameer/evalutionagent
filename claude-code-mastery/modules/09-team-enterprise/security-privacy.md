# Security, Privacy & Compliance

**Module 09, Lesson 4 — Claude Code Mastery**

**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Overview

Security and privacy are the primary gates for enterprise adoption of any AI tool. This lesson covers how Claude Code handles data privacy, credential storage, the permission system, content exclusions, the auto mode safety classifier, compliance certifications, and best practices for secure usage. Understanding these mechanisms lets security teams evaluate Claude Code with confidence.

---

## Data Privacy: How Your Code Is Handled

Claude Code operates locally on your machine. Your code stays on your filesystem — only the context needed for a specific request is sent to the Anthropic API.

| Aspect | Detail |
|--------|--------|
| Code storage | Remains on your local machine, never uploaded in bulk |
| API transmission | Only relevant snippets and conversation context are sent |
| Training data | Code sent via API is not used to train models (zero data retention for API) |
| Conversation logs | Stored locally in `~/.claude/` on your machine |
| Session persistence | Conversations are local files, not stored on Anthropic servers |

For Pro plan users, Anthropic may retain conversation data per their privacy policy. API users have zero data retention by default.

---

## Credential Storage

Claude Code stores authentication tokens securely using platform-native mechanisms:

| Platform | Storage Method | Details |
|----------|---------------|---------|
| macOS | Keychain | Stored in the system Keychain, protected by your login password |
| Linux | Encrypted file | Stored in `~/.claude/` with file-system permissions (mode 600) |
| Windows | Credential Manager | Uses Windows Credential Manager API |

Credentials are never stored in plain text, never committed to version control, and never sent as part of conversation context.

---

## Permission System as Safety Layer

Claude Code's permission system prevents unauthorized tool execution. Every tool call requires explicit approval unless pre-authorized in settings.

| Permission Level | Behavior | Configuration |
|-----------------|----------|---------------|
| Ask (default) | Prompts user before each tool execution | No configuration needed |
| Allow list | Auto-approves specific commands | `.claude/settings.json` permissions.allow |
| Deny list | Blocks specific commands entirely | `.claude/settings.json` permissions.deny |
| Auto mode | Allows all non-denied tools without prompting | Activated with `--auto` flag |

```json
{
  "permissions": {
    "allow": [
      "Bash(npm run test)",
      "Bash(npm run lint)"
    ],
    "deny": [
      "Bash(rm -rf *)",
      "Bash(curl *)",
      "Bash(git push --force)"
    ]
  }
}
```

Deny rules take precedence over allow rules. Enterprise managed policies can enforce deny rules that individual developers cannot override.

---

## Content Exclusions for Sensitive Files

Prevent Claude Code from reading files that contain secrets, credentials, or sensitive data:

```json
{
  "contentExclusions": [
    "**/*.env",
    "**/*.pem",
    "**/*.key",
    "**/secrets/**",
    "**/credentials/**",
    "**/.aws/**",
    "**/.ssh/**"
  ]
}
```

| Exclusion Scope | Files Protected | Why |
|----------------|----------------|-----|
| Environment files | `.env`, `.env.local` | API keys, database passwords |
| Certificates | `.pem`, `.key`, `.crt` | TLS certificates, private keys |
| Cloud credentials | `.aws/`, `.gcp/` | Cloud provider access tokens |
| Secret directories | `secrets/`, `credentials/` | Application secrets |

Excluded files are filtered before any content reaches the API. Claude cannot read, reference, or include them in context.

---

## Auto Mode Safety Classifier

When running in auto mode (`--auto`), Claude Code applies a safety classifier that blocks dangerous patterns:

| Blocked Pattern | Example | Reason |
|----------------|---------|--------|
| Mass file deletion | `rm -rf /`, `del /s /q` | Prevents accidental data loss |
| Network exfiltration | `curl -X POST` with file data | Prevents data leakage |
| Credential access | Reading `.ssh/id_rsa` | Protects authentication keys |
| System modification | Changing `/etc/passwd` | Prevents system compromise |
| Force push | `git push --force` to protected branches | Prevents history destruction |

The classifier runs before tool execution. Even in auto mode, commands matching dangerous patterns are rejected or escalated to manual approval.

---

## SOC 2 and HIPAA Compliance

| Certification | Status | Scope |
|--------------|--------|-------|
| SOC 2 Type II | Certified | Anthropic API infrastructure |
| HIPAA | BAA available | Enterprise plans with API access |
| GDPR | Compliant | Data processing agreements available |
| Data residency | Configurable | Route through Bedrock/Vertex for specific regions |

For organizations handling protected health information (PHI) or personally identifiable information (PII), use the API with zero data retention and route through your own cloud provider via Bedrock or Vertex model overrides.

---

## Best Practices for Secure Usage

| Practice | Implementation |
|----------|---------------|
| Use content exclusions | Block `.env`, `.pem`, `.key`, and secret directories |
| Enforce deny lists | Block destructive and network commands at enterprise level |
| Prefer API over Pro plan | Zero data retention by default for API users |
| Route through your cloud | Use Bedrock/Vertex to keep traffic in your perimeter |
| Review auto mode usage | Audit which commands run without manual approval |
| Rotate credentials regularly | Claude Code re-authenticates seamlessly after rotation |
| Enable audit logging | Track all tool executions and file access for compliance |
| Train developers | Teach teams not to paste secrets into prompts |

---

## Navigation

| Direction | Link |
|-----------|------|
| Previous | [Cost Management & Monitoring](cost-management.md) |
| Next | [Module 10: Claude Agent SDK](../10-agent-sdk/) |
| Module Home | [Module 09: Team & Enterprise](README.md) |
