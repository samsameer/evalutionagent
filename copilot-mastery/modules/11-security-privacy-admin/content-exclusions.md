# Content Exclusions

**Module 11, Lesson 2 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Content exclusions allow organizations to **prevent specific files, directories, or repositories** from being sent to Copilot. This is critical for codebases that contain sensitive information, trade secrets, or regulated data.

---

## Availability

| Plan | Content Exclusions |
|------|-------------------|
| Free | No |
| Pro | No |
| Pro+ | No |
| Business | **Yes** |
| Enterprise | **Yes** |

---

## How to Configure Content Exclusions

### Organization Level

1. Go to **Organization Settings** → **Copilot** → **Content Exclusions**
2. Add exclusion rules using glob patterns

### Repository Level

Repository admins can also configure exclusions in repository settings.

---

## Exclusion Patterns

```yaml
# Exclude specific files
- "**/.env"
- "**/.env.*"
- "**/secrets.json"
- "**/credentials.yaml"

# Exclude specific directories
- "**/internal-tools/**"
- "**/proprietary-algorithms/**"
- "**/vendor/licensed-code/**"

# Exclude by file type
- "**/*.pem"
- "**/*.key"
- "**/*.cert"

# Exclude entire repositories
- "org-name/secret-repo"
- "org-name/compliance-docs"
```

---

## What Exclusion Does

When a file matches an exclusion pattern:

| Feature | Behavior |
|---------|----------|
| **Code completions** | No suggestions shown in excluded files |
| **Copilot Chat** | Excluded files are not sent as context |
| **Agent mode** | Cannot read or modify excluded files |
| **@workspace** | Excluded files are not searchable |
| **Coding Agent** | Will not access excluded files |

---

## Common Exclusion Scenarios

### Scenario 1: Sensitive Configuration

```yaml
exclusions:
  - "**/config/production/**"
  - "**/.env*"
  - "**/secrets/**"
```

### Scenario 2: Licensed Third-Party Code

```yaml
exclusions:
  - "**/vendor/proprietary/**"
  - "**/lib/licensed/**"
```

### Scenario 3: Compliance-Regulated Code

```yaml
exclusions:
  - "**/hipaa-data/**"
  - "**/pci-processing/**"
  - "**/gdpr-handlers/**"
```

---

## Verifying Exclusions

When working in an excluded file in VS Code:

- The Copilot status bar icon will show a **disabled state**
- A tooltip will indicate that the file is excluded
- No ghost text suggestions will appear
- Copilot Chat will not include the file in context

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 11: Security & Admin](README.md) |
| Previous Lesson | [Data Privacy](data-privacy.md) |
| Next Lesson | [Organization Policies](org-policies.md) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
