# Module 06: Hooks, MCP Servers & Custom Commands

**Module 06, Overview — Claude Code Mastery**

**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Module Overview

This module covers Claude Code's extensibility layer — the systems that let you customize, automate, and integrate Claude Code into your unique development workflow. You will learn how to intercept tool execution with hooks, connect external services through MCP servers, build reusable slash commands, and leverage the skills system for on-demand expertise.

---

## Lessons in This Module

| Lesson | File | Topic | Key Concepts |
|--------|------|-------|--------------|
| 1 | [hooks-system.md](hooks-system.md) | Hooks System | PreToolUse, PostToolUse, Notification, Stop, SessionStart, environment variables, recipes |
| 2 | [mcp-servers.md](mcp-servers.md) | MCP Servers | Model Context Protocol, stdio/SSE transports, server configuration, popular servers |
| 3 | [custom-commands.md](custom-commands.md) | Custom Slash Commands | `.claude/commands/`, `$ARGUMENTS`, sharing commands, practical examples |
| 4 | [skills-system.md](skills-system.md) | Skills System | On-demand prompts, frontmatter options, skills vs CLAUDE.md, custom skills |

---

## Prerequisites

- Completed Modules 01–05 (especially the memory system and tools modules)
- A working Claude Code installation with at least one project configured
- Basic familiarity with JSON configuration files

---

## Learning Objectives

By the end of this module, you will be able to:

1. **Write hooks** that automatically lint, format, and validate code before and after tool execution
2. **Configure MCP servers** to give Claude access to GitHub, Slack, databases, and other external services
3. **Create custom slash commands** that encode your team's workflows as reusable templates
4. **Build skills** that load specialized prompts on demand without bloating every session
5. **Choose the right extensibility mechanism** (hook vs command vs skill vs CLAUDE.md) for any scenario

---

## Extensibility Decision Matrix

| Need | Mechanism | When to Use |
|------|-----------|-------------|
| Intercept/validate tool calls | **Hooks** | Auto-format on save, block dangerous commands, audit logging |
| Connect external services | **MCP Servers** | GitHub integration, database access, Slack notifications |
| Reusable prompt templates | **Custom Commands** | PR reviews, deployment checklists, testing workflows |
| On-demand specialized knowledge | **Skills** | Framework-specific guidance, domain expertise |
| Always-loaded project context | **CLAUDE.md** | Coding standards, architecture notes, team conventions |

---

## Estimated Time

| Lesson | Duration |
|--------|----------|
| Hooks System | 45 minutes |
| MCP Servers | 40 minutes |
| Custom Commands | 30 minutes |
| Skills System | 30 minutes |
| **Total** | **~2.5 hours** |

---

## Navigation

| Direction | Link |
|-----------|------|
| Previous Module | [Module 05: Tools and Workflows](../05-tools-and-workflows/) |
| Next Module | [Module 07: Advanced Features](../07-advanced-features/) |
| Home | [Course Home](../../) |
