# Knowledge Bases (Enterprise)

**Module 10, Lesson 4 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Knowledge bases are an **Enterprise-exclusive feature** that lets organizations feed custom documentation, internal wikis, API specs, and architectural documents into Copilot. This gives Copilot deep understanding of your organization's specific tools, patterns, and conventions.

---

## What Are Knowledge Bases?

Knowledge bases are collections of **Markdown documentation** from GitHub repositories that Copilot indexes and uses as context when answering questions.

```
┌─────────────────────────────────────────┐
│           Copilot Enterprise             │
│                                          │
│  Standard Context:                       │
│    - Current file                        │
│    - Open tabs                           │
│    - Workspace files                     │
│                                          │
│  + Knowledge Base Context:               │
│    - Internal API documentation          │
│    - Architecture decision records       │
│    - Style guides and coding standards   │
│    - Onboarding documentation            │
│    - Internal library documentation      │
└─────────────────────────────────────────┘
```

---

## Setting Up a Knowledge Base

### Step 1: Prepare Documentation Repositories

Create or identify repositories containing your documentation:

```
org/engineering-docs/
  architecture/
    microservices-overview.md
    database-design.md
    api-gateway.md
  standards/
    coding-standards.md
    testing-standards.md
    security-standards.md
  internal-apis/
    user-service-api.md
    payment-service-api.md
    notification-service-api.md
```

### Step 2: Create a Knowledge Base

1. Go to **Organization Settings** → **Copilot** → **Knowledge Bases**
2. Click **"New Knowledge Base"**
3. Give it a name (e.g., "Engineering Documentation")
4. Add repository sources — select the repos containing your docs
5. Configure which directories and file patterns to include
6. Click **"Create"**

### Step 3: Indexing

Copilot indexes the selected repositories:
- Markdown files (`.md`) are the primary format
- The index updates automatically when documentation changes
- Large repos may take some time for initial indexing

---

## Using Knowledge Bases in Chat

Once configured, reference knowledge bases in Copilot Chat:

```
@github Using our engineering docs, what's the standard way
to add a new microservice?

@github According to our API docs, what endpoints does the
payment service expose?

@github What are our coding standards for error handling?
```

---

## Best Practices

| Practice | Description |
|----------|-------------|
| Keep docs current | Outdated docs lead to incorrect Copilot answers |
| Use clear headings | Helps Copilot find relevant sections |
| Include code examples | Copilot uses these as patterns |
| Organize by topic | Separate architecture, API, and standards docs |
| Use Markdown | Best format for knowledge base indexing |

---

## Availability

| Feature | Plan |
|---------|------|
| Knowledge Bases | Enterprise only ($39/user/month) |
| Max repositories | Configurable per knowledge base |
| Auto-updating | Yes — re-indexes on push |
| Access control | Follows repository permissions |

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 10: Advanced Features](README.md) |
| Previous Lesson | [Prompt Files](prompt-files.md) |
| Next Lesson | [Prompt Engineering for Copilot](prompt-engineering.md) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
