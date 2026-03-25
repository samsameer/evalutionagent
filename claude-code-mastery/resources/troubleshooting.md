# Claude Code Troubleshooting Guide

**Claude Code Mastery — March 2026**
**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Installation Issues

| Problem | Cause | Solution |
|---------|-------|----------|
| `npm install -g @anthropic-ai/claude-code` fails | Insufficient permissions | Use `sudo npm install -g @anthropic-ai/claude-code` or fix your npm prefix: `npm config set prefix ~/.npm-global` |
| "Node.js version not supported" | Node.js version too old | Install Node.js 18+ via `nvm install 18` or download from nodejs.org |
| Claude Code not found after install | Binary not in PATH | Run `npm bin -g` to find the install location, then add it to your PATH |
| Installation hangs on corporate network | Proxy or firewall blocking npm | Set npm proxy: `npm config set proxy http://proxy:port` |
| Permission denied on Linux/Mac | Global npm directory ownership | Run `sudo chown -R $(whoami) $(npm config get prefix)/{lib/node_modules,bin,share}` |

## Authentication Issues

| Problem | Cause | Solution |
|---------|-------|----------|
| "Invalid API key" error | Malformed or expired key | Regenerate your key at console.anthropic.com and run `claude config set apiKey <key>` |
| OAuth login loop | Browser cookie or cache issue | Clear browser cookies for claude.ai, then retry `claude login` |
| "Rate limit exceeded" | Too many requests for your plan | Wait for the cooldown period, or upgrade your plan for higher limits |
| Authentication works but no responses | Account billing issue | Check your account balance and payment method at console.anthropic.com |
| API key not picked up in CI | Environment variable not set | Export `ANTHROPIC_API_KEY` in your CI config, or use `--api-key` flag |

## Performance Issues

| Problem | Cause | Solution |
|---------|-------|----------|
| Responses are very slow | Large context window | Run `/compact` to summarize history and free up context space |
| Claude seems to "forget" earlier instructions | Context window overflow | Use `/compact` or `/clear`. Put critical instructions in CLAUDE.md so they persist |
| High token usage and costs | Reading too many files | Be specific in prompts — tell Claude which files to look at instead of "look at the codebase" |
| Extended thinking takes too long | Complex reasoning task | Set a thinking budget with `--thinking-budget` or switch to a simpler prompt |
| Claude keeps re-reading the same files | No caching between turns | This is expected behavior — each tool call re-reads. Use `/compact` to keep summaries |
| Responses cut off mid-output | Output token limit reached | Ask Claude to continue, or increase max tokens with `--max-tokens` |

## Git Integration Issues

| Problem | Cause | Solution |
|---------|-------|----------|
| Claude won't commit changes | Permission not granted | Approve the git commit tool call, or add `git commit` to your allowlist |
| Commits have wrong author | Git config not set | Run `git config user.name "Your Name"` and `git config user.email "you@email.com"` |
| Claude creates messy commit messages | No commit conventions specified | Add commit message guidelines to your CLAUDE.md file |
| Worktree operations fail | Git worktree not initialized | Ensure you have Git 2.15+ and initialize with `git worktree add <path> <branch>` |
| Claude modifies wrong branch | Ambiguous branch context | Always specify the target branch in your prompt, or check with `git branch` first |

## MCP Issues

| Problem | Cause | Solution |
|---------|-------|----------|
| MCP server fails to start | Missing dependencies or wrong path | Check the command path in settings.json. Run the MCP server command manually to see errors |
| "Connection refused" for remote MCP | Wrong URL or server down | Verify the SSE endpoint URL and ensure the remote server is running |
| MCP tools not appearing | Server config syntax error | Validate JSON in `.claude/settings.json`. Restart Claude Code after fixing |
| MCP server crashes mid-session | Server-side bug or resource limit | Check server logs. Restart Claude Code — it will reconnect automatically |
| Environment variables not passed to MCP | Missing `env` config block | Add `"env": {"KEY": "value"}` to your MCP server config in settings.json |

## Context & CLAUDE.md Issues

| Problem | Cause | Solution |
|---------|-------|----------|
| CLAUDE.md not being read | File in wrong location | Place it in the project root (where you run `claude`) or in `~/.claude/CLAUDE.md` for global |
| CLAUDE.md instructions ignored | File too long or contradictory | Keep CLAUDE.md concise (under 200 lines). Put the most important rules first |
| Subdirectory CLAUDE.md not picked up | Not in the active working directory | Claude reads CLAUDE.md files from cwd and parent directories. Verify file location |
| Instructions conflict between CLAUDE.md files | Multiple files with contradictory rules | Use the root CLAUDE.md for global rules and subdirectory files for overrides only |
| Changes to CLAUDE.md not taking effect | Cached in current session | Run `/clear` to restart the session and force a fresh read of CLAUDE.md |

## General Tips

1. **Always update to the latest version** — Run `npm update -g @anthropic-ai/claude-code` regularly
2. **Check logs** — Claude Code stores logs in `~/.claude/logs/` for debugging
3. **Use `/doctor`** — Built-in diagnostic command that checks common configuration issues
4. **Restart fresh** — When in doubt, `/clear` the session and try again with a refined prompt
5. **Report bugs** — File issues at github.com/anthropics/claude-code with reproduction steps

---

> **Need more help?** Visit [docs.anthropic.com](https://docs.anthropic.com) or ask in the Anthropic Discord community.
