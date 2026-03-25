# Troubleshooting Guide

**Claude Code Mastery — March 2026**
**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Installation Issues

| Problem | Solution |
|---------|----------|
| `npm install -g @anthropic-ai/claude-code` fails with permission error | Use `sudo npm install -g @anthropic-ai/claude-code` or fix npm permissions with `npm config set prefix ~/.npm-global` and add to PATH |
| "Node.js version not supported" | Claude Code requires Node.js 18+. Update with `nvm install 20 && nvm use 20` |
| Installation hangs on corporate network | Configure npm proxy: `npm config set proxy http://proxy.company.com:8080` |
| Claude command not found after install | Ensure npm global bin is in PATH: `export PATH="$(npm prefix -g)/bin:$PATH"` |
| Conflicts with existing `claude` command | Uninstall conflicting packages. Check with `which claude` to identify the conflict |

## Authentication Issues

| Problem | Solution |
|---------|----------|
| "Invalid API key" error | Verify key starts with `sk-ant-`. Re-export: `export ANTHROPIC_API_KEY=sk-ant-...` |
| Key works in API but not Claude Code | Ensure no trailing whitespace in the key. Check with `echo "$ANTHROPIC_API_KEY" | cat -A` |
| OAuth login fails | Clear cached credentials: `rm -rf ~/.claude/auth*` and retry `claude login` |
| "Rate limit exceeded" | You have hit API rate limits. Wait 60 seconds or upgrade your API plan for higher limits |
| Bedrock authentication error | Verify AWS credentials: `aws sts get-caller-identity`. Ensure IAM role has `bedrock:InvokeModel` permission |
| Vertex AI 403 error | Check GCP project has Vertex AI API enabled and service account has `aiplatform.endpoints.predict` role |

## Performance Issues

| Problem | Solution |
|---------|----------|
| Responses are very slow | Check internet connection. Use `/cost` to see if context is large. Run `/compact` to reduce context |
| Claude gets stuck in a loop | Press `Ctrl+C` to interrupt, then rephrase your request more specifically. Add constraints to CLAUDE.md |
| High token usage / expensive sessions | Use `/compact` regularly. Be specific in prompts. Avoid "fix everything" requests. Set `--max-turns` |
| Context window full (auto-compaction triggered) | This is normal for long sessions. Start a new session with `/clear` for fresh context |
| Extended thinking makes responses too slow | Disable with `--no-thinking` for simpler tasks. Reserve extended thinking for complex debugging |
| Subagents spawning excessively | Add `Limit subagent usage` to CLAUDE.md or reduce task scope in your prompts |

## Git Integration Issues

| Problem | Solution |
|---------|----------|
| Claude does not see recent Git changes | Run `git status` manually first. Claude reads the working directory state at the time of each tool call |
| Merge conflicts after Claude's changes | Use standard Git conflict resolution. Claude can help: "Resolve the merge conflicts in file.ts" |
| Claude commits to wrong branch | Always specify the branch in your prompt. Add branch conventions to CLAUDE.md |
| Worktree commands fail | Ensure Git 2.15+ is installed. Check existing worktrees with `git worktree list` |
| Claude refuses to force-push | This is a safety feature. Explicitly say "force push to branch X" if you truly need it |

## MCP Issues

| Problem | Solution |
|---------|----------|
| MCP server fails to start | Check the command path exists. Test manually: run the MCP server command in terminal |
| "Tool not found" for MCP tools | Verify server is listed in `.claude/settings.json`. Restart Claude Code after config changes |
| MCP server crashes mid-session | Claude Code will show an error. Restart the session. Check MCP server logs for the crash cause |
| Timeout connecting to MCP server | Increase timeout in settings. Ensure the MCP server process starts within 10 seconds |
| MCP tools return unexpected results | Test the MCP server independently. Check input/output schemas match expectations |

## Context & Memory Issues

| Problem | Solution |
|---------|----------|
| Claude ignores CLAUDE.md instructions | Ensure the file is named exactly `CLAUDE.md` (case-sensitive) in the project root. Check for syntax errors |
| CLAUDE.md not loading | Verify you launched Claude Code from the directory containing CLAUDE.md or a subdirectory |
| Claude forgets earlier conversation | Context was compacted. Re-state important points or add them to CLAUDE.md for persistence |
| Too many CLAUDE.md files causing conflicts | Use clear scoping: root CLAUDE.md for project-wide rules, subdirectory files for local overrides |
| Global settings not applying | Check `~/.claude/CLAUDE.md` exists and has correct permissions (`chmod 644`) |

## Common Error Messages

| Error | Meaning & Fix |
|-------|--------------|
| `ECONNREFUSED` | Cannot reach API endpoint. Check internet connection and proxy settings |
| `context_length_exceeded` | Conversation too long. Run `/compact` or start a new session |
| `overloaded_error` | Anthropic API is under heavy load. Wait 30-60 seconds and retry |
| `invalid_request_error` | Malformed request. Update Claude Code to latest version: `npm update -g @anthropic-ai/claude-code` |
| `permission_denied` | Claude tried a tool you have not approved. Grant permission or add to allowlist |

---

> **Tip:** Run `claude --version` and include the output when reporting issues. Most problems are resolved by updating to the latest version.
