# Troubleshooting Guide

**Module 11, Lesson 4 — Claude Code Mastery**

**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Overview

When something goes wrong with Claude Code, this decision tree helps you diagnose and fix the issue quickly. Start with the symptom that matches your situation and follow the steps.

---

## 0. First Step: Run /doctor

Before diving into specific issues, run the built-in diagnostic command:

```
/doctor
```

This checks your installation, authentication, connectivity, and configuration. Fix anything it flags before proceeding with manual troubleshooting below.

---

## 1. Installation Issues

**Symptom:** `claude` command not found or installation fails.

| Check | Fix |
|-------|-----|
| Is Node.js 18+ installed? | Run `node --version`. If below 18, upgrade Node.js. |
| Was npm install successful? | Re-run `npm install -g @anthropic-ai/claude-code`. |
| Is the npm global bin in PATH? | Run `npm bin -g` and verify that directory is in your `$PATH`. |
| Permission denied on global install? | Use `sudo npm install -g @anthropic-ai/claude-code` or fix npm permissions with `npm config set prefix ~/.npm-global` and add `~/.npm-global/bin` to PATH. |
| Using nvm and command disappears? | Run `nvm alias default node` to set a persistent default. |
| Corporate firewall blocking npm? | Set npm registry: `npm config set registry https://registry.npmjs.org/` and configure proxy: `npm config set proxy http://proxy:8080`. |

---

## 2. Authentication Problems

**Symptom:** "Invalid API key", "Unauthorized", or login fails.

| Check | Fix |
|-------|-----|
| API key set correctly? | Run `echo $ANTHROPIC_API_KEY` to verify. It should start with `sk-ant-`. |
| Key expired or revoked? | Generate a new key at console.anthropic.com. |
| Using OAuth login? | Run `/login` and follow the browser flow. Check that the browser opened correctly. |
| Behind a proxy? | Set `HTTP_PROXY` and `HTTPS_PROXY` environment variables. |
| Bedrock auth failing? | Verify `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`, and `AWS_REGION` are set. Run `aws sts get-caller-identity` to test. |
| Vertex AI auth failing? | Verify `CLOUD_ML_REGION` and `ANTHROPIC_VERTEX_PROJECT_ID` are set. Run `gcloud auth print-access-token` to test. |
| API key helper failing? | Test your `apiKeyHelper` command manually in a terminal. Check `CLAUDE_CODE_API_KEY_HELPER_TTL_MS`. |

---

## 3. Permission Errors

**Symptom:** Claude says "permission denied" or a tool call is blocked.

| Check | Fix |
|-------|-----|
| Permission mode too restrictive? | Check with `/status`. Switch mode: `--permission-mode auto-edit`. |
| Deny rule blocking the action? | Check `/permissions` and your `settings.json` for `permissions.deny` entries. |
| File system permissions? | Ensure Claude Code's process can read/write the target files. Check with `ls -la`. |
| Enterprise policy blocking? | Check `/etc/claude/settings.json` or managed policy for deny rules. Contact your admin. |
| Hook blocking the tool? | A `PreToolUse` hook returning exit code 2 blocks the action. Check your hooks config. |

---

## 4. Context Window Full

**Symptom:** "Context window is full" or Claude starts forgetting earlier parts of the conversation.

| Check | Fix |
|-------|-----|
| Long conversation? | Run `/compact` to condense the conversation. Optionally add a focus: `/compact focus on auth module`. |
| Need a fresh start? | Run `/clear` to reset the conversation entirely. |
| Reading too many large files? | Be specific about which files to read. Use line ranges: "Read lines 50-100 of file.ts". |
| Repeatedly hitting the limit? | Break your work into smaller sessions. Use CLAUDE.md to carry context between sessions. |
| Cost increasing rapidly? | Check `/cost`. Large context means more tokens per message. Compact regularly. |

---

## 5. Claude Not Following Instructions

**Symptom:** Claude ignores your conventions, uses wrong patterns, or produces off-target results.

| Check | Fix |
|-------|-----|
| Instructions in CLAUDE.md? | Verify your CLAUDE.md exists and is in the right location (project root or `~/.claude/`). |
| CLAUDE.md too long? | Keep it focused. Claude weighs recent/relevant instructions more heavily. |
| Conflicting instructions? | Check all CLAUDE.md scopes (user, project, directory). Remove contradictions. |
| Prompt too vague? | Be specific. See the Prompt Engineering lesson for templates. |
| Wrong model? | Check `/status`. Some models follow instructions more precisely than others. Use `opus` for complex instructions. |
| Context window full of noise? | Run `/compact` to clear irrelevant history and refocus. |

---

## 6. MCP Server Connection Issues

**Symptom:** MCP tools not appearing, server fails to start, or "MCP server disconnected".

| Check | Fix |
|-------|-----|
| Server configured correctly? | Check `mcpServers` in your settings.json. Verify `command` and `args`. |
| npx failing? | Run the MCP server command manually to see error output: `npx -y @modelcontextprotocol/server-name`. |
| Missing environment variables? | MCP servers often need API tokens. Check the `env` field in your server config. |
| Server crashing on start? | Check server logs. Run the command manually with verbose output. |
| Port conflict? | If the server uses a port, check for conflicts: `lsof -i :PORT`. |
| Wrong settings file? | MCP servers must be in `~/.claude/settings.json` (user) or `.claude/settings.json` (project). Not in CLAUDE.md. |
| Server appears but tools are missing? | The server may be running but not registering tools. Check server documentation for required setup. |

---

## 7. Slow Responses

**Symptom:** Claude takes a long time to respond or seems to hang.

| Check | Fix |
|-------|-----|
| Large context window? | Run `/compact` to reduce context size. Smaller context = faster responses. |
| Network issues? | Check your internet connection. Try `curl https://api.anthropic.com`. |
| Using a proxy? | Proxies add latency. Test without proxy if possible. |
| Opus model? | Opus is slower than Sonnet. Switch to `sonnet` for faster responses on simpler tasks. |
| Rate limited? | Check for rate limit messages. Wait and retry, or upgrade your plan. |
| Many tool calls? | Complex tasks with many file reads/writes take time. This is normal. |

---

## 8. High Costs

**Symptom:** API costs are higher than expected.

| Check | Fix |
|-------|-----|
| Using Opus for everything? | Switch to `sonnet` for routine tasks. Reserve `opus` for complex reasoning. |
| Large context window? | Use `/compact` regularly. Every message with a large context costs more. |
| Not using `/compact`? | After completing a subtask, compact before starting the next one. |
| Runaway automation? | Set `--max-turns` to limit agentic loops: `claude --max-turns 10 -p "task"`. |
| Check current costs | Run `/cost` to see token usage and estimated cost for the current session. |
| Set up cost alerts | Monitor usage at console.anthropic.com. Set spending limits on your API key. |
| Caching disabled? | Prompt caching reduces costs for repeated context. Do not use `--no-cache` unless necessary. |

---

## 9. Git Integration Issues

**Symptom:** Claude creates wrong commits, misses files, or git operations fail.

| Check | Fix |
|-------|-----|
| Not in a git repo? | Run `git status` to verify. Claude Code works best inside git repos. |
| Uncommitted changes before starting? | Commit or stash your work before asking Claude to make changes. This makes it easy to revert. |
| Claude committed wrong files? | Use `git diff HEAD~1` to review. Revert with `git reset HEAD~1` if needed. |
| Merge conflicts? | Claude can help resolve them: "Resolve the merge conflicts in src/app.ts preferring our changes." |
| Git hooks failing? | Check `.git/hooks/` or `.husky/` for pre-commit hooks that may reject Claude's changes. |

---

## 10. Quick Diagnostic Checklist

When nothing above matches, run through this checklist:

```
1. [ ] Run /doctor
2. [ ] Check /status for model, mode, and context usage
3. [ ] Check /cost for unexpected token consumption
4. [ ] Verify ANTHROPIC_API_KEY is set: echo $ANTHROPIC_API_KEY
5. [ ] Verify Node.js version: node --version (must be 18+)
6. [ ] Verify Claude Code version: claude --version
7. [ ] Check settings: cat ~/.claude/settings.json
8. [ ] Check project settings: cat .claude/settings.json
9. [ ] Check CLAUDE.md: cat CLAUDE.md
10.[ ] Try a fresh session: claude --no-cache
11.[ ] Update Claude Code: npm update -g @anthropic-ai/claude-code
12.[ ] Check Anthropic status page: status.anthropic.com
```

---

## Navigation

| Direction | Link |
|-----------|------|
| Previous Lesson | [Prompt Engineering](prompt-engineering.md) |
| Next Lesson | [Module 12: Real-World Projects](../12-real-world-projects/) |
| Module Overview | [Module 11: Cheat Sheets](README.md) |

---

> **Tip:** Most Claude Code issues fall into three categories: authentication, context window, and prompt quality. Master those three and you will rarely need this page.
