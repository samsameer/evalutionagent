# Web Search & Fetch

**Module 05, Lesson 5 — Claude Code Mastery**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Claude Code can reach beyond your local filesystem and access the web. The **WebSearch** and **WebFetch** tools let you search for information online and read web pages directly within your development session. This turns Claude from a local code assistant into a connected development partner that can look up documentation, research error messages, and pull in external knowledge on demand.

---

## WebSearch

WebSearch queries the web and returns relevant results. It is the equivalent of opening a browser and searching — but the results flow directly into your Claude session.

### When to Use WebSearch

| Scenario | Example Prompt |
|----------|---------------|
| Debug an error message | "Search the web for 'TypeError: Cannot read property of undefined React 18'" |
| Find a library or tool | "Search for the best Node.js rate limiting libraries in 2026" |
| Check for known issues | "Search for known issues with PostgreSQL 16 and Node.js connection pooling" |
| Look up best practices | "Search for TypeScript monorepo best practices" |
| Find CVEs or security advisories | "Search for recent CVEs in the lodash npm package" |
| Research an unfamiliar concept | "Search for 'CQRS event sourcing pattern explained'" |

### Tips for Effective Searches

1. **Be specific** — Include version numbers, framework names, and error codes
2. **Use quotes for exact phrases** — "Search for 'useEffect cleanup race condition'"
3. **Include context** — "Search for Next.js 14 app router middleware authentication"
4. **Ask Claude to search when stuck** — "I'm getting this error, search the web for solutions"

### Example Workflow

```
You: This build is failing with "Module not found: Can't resolve 'node:crypto'".
     Search for what causes this.

Claude: [Uses WebSearch to find results]
        This error occurs when bundling Node.js-only modules for the browser.
        The 'node:crypto' protocol prefix was added in Node.js 16. The fix is
        to add a fallback in your webpack/vite config...
```

---

## WebFetch

WebFetch retrieves the content of a specific URL. It is the equivalent of visiting a page and reading it — Claude gets the full text content for analysis.

### When to Use WebFetch

| Scenario | Example Prompt |
|----------|---------------|
| Read API documentation | "Fetch the Stripe API docs for payment intents" |
| Read a GitHub issue | "Fetch https://github.com/org/repo/issues/42 and summarize it" |
| Read a changelog | "Fetch the Next.js 15 release notes and tell me what changed" |
| Pull in a config example | "Fetch the official ESLint flat config migration guide" |
| Read a blog post or tutorial | "Fetch this article and apply its pattern to our code" |
| Review a package README | "Fetch the npm page for zod and explain its validation API" |

### Tips for Effective Fetching

1. **Provide the full URL** — Claude needs the exact page to fetch
2. **Ask for specific information** — "Fetch this page and tell me how to configure X"
3. **Chain with actions** — "Fetch the docs and then implement the pattern in our code"
4. **Use for verification** — "Fetch the official docs to check if my implementation is correct"

---

## Combining Web Tools with Development

The real power of web tools emerges when you combine them with code editing. Here are common patterns:

### Pattern 1: Research Then Implement

```
You: We need to add WebSocket support. Search for the best approach
     with our Express + TypeScript stack, then implement it.

Claude:
  1. [WebSearch] Finds that "ws" library is the standard choice
  2. [WebFetch] Reads the ws library documentation
  3. [Bash] Runs npm install ws @types/ws
  4. [Write] Creates src/websocket/server.ts
  5. [Edit] Integrates WebSocket server with Express app
  6. [Bash] Runs tests
```

### Pattern 2: Debug with Online Context

```
You: Our JWT validation is rejecting valid tokens after the server restarts.
     Figure out why.

Claude:
  1. [Grep] Finds JWT validation code
  2. [Read] Reads the implementation
  3. [WebSearch] Searches for "JWT validation fails after server restart"
  4. [Analysis] Identifies that the signing key is generated at runtime
     instead of loaded from environment
  5. [Edit] Fixes the code to use a persistent key
```

### Pattern 3: API Documentation Lookup

```
You: Add a function to fetch the current weather using the OpenWeatherMap API.

Claude:
  1. [WebFetch] Fetches OpenWeatherMap API documentation
  2. [Read] Reads existing API utility patterns in the project
  3. [Write] Creates src/services/weather.ts matching project conventions
  4. [Write] Creates src/services/weather.test.ts
```

### Pattern 4: Staying Current

```
You: Check if there are any breaking changes in React 19 that affect
     our codebase.

Claude:
  1. [WebSearch] Searches for "React 19 breaking changes migration guide"
  2. [WebFetch] Reads the official migration guide
  3. [Grep] Searches codebase for affected APIs
  4. [Read] Reviews each affected file
  5. [Summary] Reports which files need changes and what to update
```

---

## Piping Web Content into Analysis

One powerful workflow is fetching web content and having Claude analyze it against your codebase:

```
Fetch the OWASP Top 10 for 2025 and audit our authentication
module against each item.
```

Claude will:

1. **WebFetch** the OWASP page
2. **Glob** and **Read** your auth-related files
3. Produce a security audit comparing your code against each OWASP category

This same pattern works for:

| Use Case | Prompt Pattern |
|----------|---------------|
| Compliance checks | "Fetch the accessibility guidelines and check our components" |
| Style guide enforcement | "Fetch the Airbnb style guide and compare our ESLint config" |
| Dependency audits | "Fetch the advisory page for X and check if we're affected" |
| Performance benchmarks | "Fetch the Web Vitals documentation and audit our pages" |

---

## Limitations and Considerations

| Limitation | Detail |
|------------|--------|
| **No persistent browsing** | Each fetch is independent; there is no session or cookie state |
| **No JavaScript rendering** | WebFetch gets the raw HTML/text, not JavaScript-rendered content |
| **Rate limits** | Excessive fetching may hit rate limits on target sites |
| **Content size** | Very large pages may be truncated |
| **Authentication** | Cannot fetch pages that require login |

### When Web Tools Are Not the Right Choice

- **Private documentation** — Use Read to access local docs instead
- **Frequently changing data** — Results may be stale by the time you act on them
- **Large file downloads** — Use Bash with `curl` or `wget` for binary downloads

---

## Best Practices

1. **Search first, fetch second** — Use WebSearch to find the right page, then WebFetch to read it
2. **Be specific about what you need** — "Fetch this URL and tell me the rate limit headers" is better than "fetch this"
3. **Combine with local context** — The best results come from comparing web content against your actual code
4. **Verify before implementing** — Cross-reference multiple sources for critical decisions
5. **Use for learning** — Ask Claude to fetch tutorials and explain concepts in the context of your project

---

[← Code Editing Workflows](code-editing.md) | [Module 06: Hooks, MCP & Commands →](../06-hooks-mcp-commands/README.md)

---

*Module 05, Lesson 5 — Claude Code Mastery — March 2026*
