# Claude Code — Frequently Asked Questions

**Claude Code Mastery — March 2026**
**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Privacy & Security

### 1. Is my code sent to Anthropic?

Yes — code that Claude reads is sent to Anthropic's API for processing. However, Anthropic does not train on API data by default. If you use Claude Code through a Max subscription or API key, your inputs and outputs are not used for model training unless you explicitly opt in. Review Anthropic's data usage policy for your plan.

### 2. Is Claude Code safe to use on proprietary codebases?

Yes, with appropriate plan selection. Enterprise and API plans include contractual commitments that data is not used for training. Use the `--no-telemetry` flag to disable anonymous usage analytics if required by your organization.

### 3. Are my conversations stored locally?

Yes. Conversation history is stored locally on your machine in `~/.claude/` and is never uploaded. You can resume previous sessions with `claude --resume`.

---

## Models & Pricing

### 4. Which model does Claude Code use?

Claude Code defaults to Claude Sonnet (currently claude-sonnet-4-20250514). You can switch to Opus for complex tasks using `/model` or the `--model` flag. Haiku is available for lighter tasks.

### 5. How much does Claude Code cost?

Claude Code is available through a Max subscription ($100/month or $200/month for higher limits) or via API pay-as-you-go pricing. Typical coding sessions cost $0.50-$5.00 depending on complexity and context size.

### 6. How do I reduce token costs?

- Keep CLAUDE.md files concise and relevant
- Use `/compact` regularly to summarize conversation history
- Use `/clear` to start fresh when switching tasks
- Enable prompt caching by maintaining consistent context prefixes
- Avoid pasting large files — let Claude read only what it needs

### 7. What is the difference between Sonnet and Opus?

Sonnet is faster and cheaper, ideal for most coding tasks. Opus provides deeper reasoning for complex architecture decisions, subtle bugs, and multi-file refactors. Use Sonnet by default and switch to Opus when Sonnet struggles.

---

## Usage & Features

### 8. Can I use Claude Code offline?

No. Claude Code requires an internet connection to communicate with Anthropic's API. There is no local model option.

### 9. What programming languages does Claude Code support?

Claude Code works with any text-based programming language. It has strong capabilities in Python, JavaScript/TypeScript, Go, Rust, Java, C/C++, Ruby, PHP, Swift, and more. It can also work with configuration files, markup languages, and shell scripts.

### 10. Can Claude Code run my tests and fix failures?

Yes. Claude Code can execute test suites, read failure output, diagnose issues, and apply fixes — all in a single agentic loop. Use a prompt like: "Run the test suite and fix any failing tests."

### 11. How do I give Claude project-specific instructions?

Create a `CLAUDE.md` file in your project root. Claude Code reads this automatically at the start of every session. Include coding conventions, architecture notes, build commands, and common patterns.

### 12. Can Claude Code work with monorepos?

Yes. Place a root-level `CLAUDE.md` with global conventions, then add `CLAUDE.md` files in subdirectories for package-specific instructions. Claude Code merges them based on the working directory.

### 13. What are hooks and when should I use them?

Hooks are shell commands that run before or after Claude Code events. Use them to auto-lint after file edits, auto-format code, block dangerous commands, or send notifications when tasks complete. Configure them in `.claude/settings.json`.

---

## Troubleshooting

### 14. Why does Claude Code lose context mid-conversation?

The context window has a finite size. Long sessions with many file reads and tool calls fill it up. Use `/compact` to summarize and reclaim space, or `/clear` to start fresh.

### 15. Why is Claude Code slow?

Common causes: large context windows, extended thinking on complex tasks, rate limiting on your plan, or slow network. Try `/compact` to reduce context size, or check your plan's rate limits.

### 16. Can I use Claude Code in CI/CD pipelines?

Yes. Use headless mode: `claude -p "your prompt" --output-format json`. Set your API key via the `ANTHROPIC_API_KEY` environment variable. This is ideal for automated code review, test generation, and migration scripts.

### 17. Does Claude Code work with VS Code and JetBrains?

Yes. Claude Code has official extensions for both VS Code and JetBrains IDEs that embed the terminal experience directly in your editor with additional GUI features.

### 18. Can multiple team members share a CLAUDE.md?

Yes — commit CLAUDE.md to version control. The team shares project conventions while individual preferences go in `~/.claude/CLAUDE.md` (the user-level file).

### 19. How do I use MCP servers with Claude Code?

Add MCP server configurations to `.claude/settings.json` under the `mcpServers` key. Each server needs a command, arguments, and optional environment variables. Claude Code connects to them automatically on startup.

### 20. What is the maximum file size Claude Code can handle?

Claude Code can read any file, but very large files consume significant context. For files over 1,000 lines, Claude typically reads only the relevant sections. There is no hard file-size limit, but practical limits are governed by the context window.

---

> **Still have questions?** Run `/help` in Claude Code or visit [docs.anthropic.com](https://docs.anthropic.com).
