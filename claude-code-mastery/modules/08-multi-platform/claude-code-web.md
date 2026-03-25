# Claude Code on the Web (claude.ai/code)

**Module 08, Lesson 1 — Claude Code Mastery**

**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Overview

Claude Code on the Web brings the full agentic coding experience into your browser at **claude.ai/code**. Instead of running on your local machine, it operates inside a cloud-hosted container (sandbox) where Claude can read files, write code, execute commands, and install packages — all without touching your local environment. This lesson covers how the web experience works, how it differs from the CLI, and when to use it.

---

## What Is claude.ai/code?

Claude Code on the Web is a browser-based version of Claude Code. When you start a session, Anthropic provisions a sandboxed Linux container in the cloud. Claude has full access to that container — it can create files, run shell commands, install dependencies, and build projects just like it would on your local machine.

| Aspect | Detail |
|--------|--------|
| URL | `https://claude.ai/code` |
| Environment | Cloud-hosted Linux container |
| Persistence | Files persist for the duration of the session |
| Access | Available to Claude Pro, Team, and Enterprise plans |
| Local files | Not accessible — must upload or clone from a repo |

---

## Container and Sandbox Environment

Each web session runs in an isolated container with its own filesystem, network access, and shell. This sandbox is pre-configured with common development tools.

**Pre-installed tools typically include:**

```
node, npm, npx        # JavaScript / TypeScript
python3, pip           # Python
git                    # Version control
curl, wget             # HTTP clients
gcc, make              # C/C++ build tools
```

Claude can install additional packages as needed using `apt`, `pip`, `npm`, or other package managers.

---

## How It Differs from the CLI

| Feature | CLI (Local) | Web (claude.ai/code) |
|---------|-------------|----------------------|
| Runs on | Your machine | Cloud container |
| File access | Full local filesystem | Sandbox only |
| MCP servers | Full support | Limited |
| Hooks | All hook types | SessionStart only |
| CLAUDE.md | Read from project | Must be uploaded or created |
| Git integration | Works with local repos | Must clone inside sandbox |
| Session duration | Until you exit | Time-limited by plan |
| Performance | Depends on your machine | Consistent cloud hardware |

---

## SessionStart Hooks for Web Environment Setup

Since the web environment starts fresh each session, **SessionStart hooks** are particularly useful for configuring the sandbox automatically. You can define them in a `settings.json` that gets loaded at session start.

```json
{
  "hooks": {
    "SessionStart": [
      {
        "matcher": "",
        "hooks": [
          {
            "type": "command",
            "command": "pip install pytest black ruff && npm install -g typescript"
          }
        ]
      }
    ]
  }
}
```

Common SessionStart tasks for web sessions:

| Task | Example Command |
|------|-----------------|
| Install Python tools | `pip install pytest flask black` |
| Install Node tools | `npm install -g typescript eslint` |
| Clone a repository | `git clone https://github.com/user/repo.git` |
| Set environment variables | `export DATABASE_URL=...` |
| Configure git identity | `git config --global user.name "Name"` |

---

## File Upload and Project Setup

There are several ways to get your code into a web session:

1. **Upload files** — Drag and drop files or folders directly into the chat interface.
2. **Clone from Git** — Ask Claude to clone a repository by providing the URL.
3. **Create from scratch** — Describe what you want and let Claude generate the project.
4. **Paste code** — Paste code snippets directly into the conversation.

```
# Example: asking Claude to set up a project
> Clone https://github.com/my-org/my-api.git and install dependencies
```

---

## Limitations Compared to the CLI

- **No local file access** — Claude cannot read or modify files on your machine.
- **No persistent environment** — Installed packages and files do not carry over between sessions.
- **Limited hook support** — Only SessionStart hooks are available; PreToolUse, PostToolUse, and other hooks are not supported.
- **No custom MCP servers** — You cannot connect your own MCP servers running locally.
- **Session time limits** — Sessions may be reclaimed after a period of inactivity.
- **No hardware peripherals** — No access to local GPUs, USB devices, or other hardware.

---

## Best Use Cases

| Use Case | Why the Web Works Well |
|----------|------------------------|
| Quick prototyping | Zero setup — start coding immediately |
| Code review and exploration | Upload a repo and ask questions |
| Learning and experimentation | Safe sandbox with no risk to your machine |
| Sharing sessions | Easy to share results without local setup |
| Working from any device | Only needs a browser — no install required |
| Building standalone scripts | Self-contained work that does not need local files |

---

## Navigation

| Direction | Link |
|-----------|------|
| Previous | [Module Overview](README.md) |
| Next | [VS Code Extension](vs-code-extension.md) |
| Home | [Course Home](../../) |
