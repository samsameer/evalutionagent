# Troubleshooting Guide

**GitHub Copilot Mastery — March 2026**

---

## Common Issues and Solutions

### Issue: No Inline Suggestions Appearing

| Check | Solution |
|-------|----------|
| Extension installed? | Install "GitHub Copilot" from VS Code Marketplace |
| Signed in? | Click the Copilot icon in status bar → Sign in |
| Subscription active? | Check at github.com/settings/copilot |
| File type enabled? | Check `github.copilot.enable` in settings |
| Internet connected? | Copilot requires a network connection |
| VS Code updated? | Update to latest version |

### Issue: Copilot Chat Not Working

| Check | Solution |
|-------|----------|
| Chat extension installed? | Install "GitHub Copilot Chat" extension |
| Agent mode not showing? | Update VS Code to 1.95+ and enable `chat.agent.enabled` |
| Model not available? | Check your plan supports the selected model |
| Chat panel empty? | Close and reopen the chat panel |

### Issue: Agent Mode Not Available

| Check | Solution |
|-------|----------|
| VS Code version | Update to 1.95 or later |
| Setting enabled? | Set `chat.agent.enabled: true` |
| Plan supports it? | Available on Pro, Pro+, Business, Enterprise |
| Correct mode? | Click mode selector at top of chat → "Agent" |

### Issue: MCP Server Not Connecting

| Check | Solution |
|-------|----------|
| MCP enabled? | Set `chat.mcp.enabled: true` in settings |
| Config correct? | Verify `.vscode/mcp.json` syntax |
| Server package exists? | Run `npx -y @modelcontextprotocol/server-xxx` manually |
| Environment variables? | Check API keys and tokens are set |
| Reload needed? | Reload VS Code window after config changes |

### Issue: Copilot CLI Not Working

| Check | Solution |
|-------|----------|
| GitHub CLI installed? | Run `gh --version` — install if missing |
| Authenticated? | Run `gh auth login` |
| Extension installed? | Run `gh extension install github/gh-copilot` |
| Plan supports CLI? | CLI requires Pro, Pro+, Business, or Enterprise |

### Issue: Suggestions Are Low Quality

| Possible Cause | Solution |
|----------------|----------|
| Insufficient context | Keep related files open in editor tabs |
| No comments | Add descriptive comments before functions |
| Vague variable names | Use descriptive names that convey intent |
| Wrong model | Try switching to a different AI model |
| Missing custom instructions | Create `.github/copilot-instructions.md` |

### Issue: Copilot Coding Agent Failed

| Check | Solution |
|-------|----------|
| Setup steps configured? | Create `.github/copilot-setup-steps.yml` |
| Dependencies installable? | Verify build works in a clean environment |
| Issue well-written? | Provide clear requirements and acceptance criteria |
| Secrets available? | Configure needed secrets in repository settings |
| Timeout? | Simplify the task or break it into smaller issues |

---

## Getting Help

1. **GitHub Copilot Documentation:** [docs.github.com/copilot](https://docs.github.com/copilot)
2. **GitHub Community:** [github.community](https://github.community)
3. **VS Code Copilot Issues:** [github.com/orgs/community/discussions](https://github.com/orgs/community/discussions)
4. **GitHub Support:** [support.github.com](https://support.github.com)

---

[← Back to Course Home](../README.md)

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
