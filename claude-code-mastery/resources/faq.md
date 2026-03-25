# Frequently Asked Questions

**Claude Code Mastery — March 2026**
**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Privacy & Security

### 1. Is my code sent to Anthropic?
Yes, code snippets are sent to Anthropic's API for processing. However, Anthropic does not train on API data. For enterprise compliance, use AWS Bedrock or Google Vertex AI as intermediaries so code never reaches Anthropic servers directly.

### 2. Are my conversations stored?
Conversations are stored locally in `~/.claude/projects/`. Anthropic may retain API logs for 30 days for abuse monitoring but does not use them for training. You can clear local history with `/clear` or by deleting the project folder.

### 3. Can I use Claude Code in air-gapped environments?
Not directly. Claude Code requires internet access to reach the Anthropic API (or Bedrock/Vertex endpoints). For restricted environments, configure a proxy or use Bedrock within your AWS VPC.

## Models & Pricing

### 4. Which model does Claude Code use?
By default, Claude Code uses Claude Sonnet (the latest version). You can override this with `CLAUDE_MODEL` environment variable to use Opus for complex tasks or Haiku for faster, cheaper operations.

### 5. How do I reduce costs?
- Use `/compact` frequently to reduce context size
- Write specific, focused prompts instead of vague requests
- Use `--max-turns` in headless mode to cap iterations
- Enable prompt caching by keeping CLAUDE.md stable across sessions
- Use Haiku for simple tasks, Sonnet for standard work, Opus for complex reasoning

### 6. How much does Claude Code cost?
Claude Code itself is free and open source. You pay for API usage: Sonnet costs approximately $3/$15 per million input/output tokens. A typical coding session uses $0.50-$5.00 depending on complexity and context size.

## Setup & Configuration

### 7. Can I use Claude Code offline?
No. Claude Code requires an active internet connection to communicate with the Claude API. All reasoning happens server-side.

### 8. How do I set up Claude Code with VS Code?
Install the "Claude Code" extension from the VS Code marketplace. It embeds Claude Code as a panel within VS Code. Alternatively, use Claude Code in the integrated terminal directly.

### 9. Does Claude Code work with JetBrains IDEs?
Yes. Install the Claude Code plugin from the JetBrains marketplace. It supports IntelliJ, PyCharm, WebStorm, GoLand, and other JetBrains products.

### 10. How do I configure Claude Code for my team?
Create a `.claude/settings.json` at the project root with shared configuration. Use enterprise OAuth/SSO for authentication. Distribute a shared CLAUDE.md with team conventions.

## Usage & Capabilities

### 11. What programming languages does Claude Code support?
Claude Code is language-agnostic. It supports any language that Claude understands, including Python, JavaScript/TypeScript, Go, Rust, Java, C/C++, Ruby, PHP, Swift, Kotlin, and many more. Effectiveness varies by language popularity in training data.

### 12. Can Claude Code run my tests?
Yes. Claude Code can execute shell commands including test runners. Configure your test command in CLAUDE.md so Claude knows how to run tests for your project (e.g., `npm test`, `pytest`, `go test`).

### 13. How do I give Claude Code access to databases or APIs?
Use MCP (Model Context Protocol) servers. Configure them in `.claude/settings.json` to expose database queries, API calls, or other external tools to Claude during your session.

### 14. Can Claude Code work with multiple files?
Yes. Claude Code excels at multi-file changes. It can read, create, and edit files across your entire project. For large refactors, provide clear instructions and let Claude plan the changes.

### 15. How does context window management work?
Claude Code automatically manages context. When the window fills up, it triggers auto-compaction (summarizing older parts of the conversation). You can manually trigger this with `/compact`. CLAUDE.md content is always preserved.

### 16. Can I use Claude Code in CI/CD pipelines?
Yes. Use headless mode: `claude -p "your prompt" --max-turns 10 --allowedTools bash,write`. This runs non-interactively and returns the result to stdout. Ideal for automated code review, test generation, and migrations.

### 17. How do I undo changes Claude made?
Claude Code works with your normal Git workflow. Use `git diff` to review changes and `git checkout -- .` to revert. Claude also shows diffs before applying changes, so you can reject modifications.

### 18. What is the maximum file size Claude can handle?
Claude can read files of any size, but very large files consume significant context. For files over 1000 lines, Claude Code automatically reads relevant sections rather than the entire file. Point Claude to specific line ranges for best results.

### 19. Can multiple people use Claude Code on the same project simultaneously?
Yes. Each person runs their own Claude Code session with their own API key. Use Git branches to avoid conflicts. Claude Code does not lock files or interfere with other sessions.

### 20. How do I report bugs or request features?
File issues on the Claude Code GitHub repository at `github.com/anthropics/claude-code`. Include your Claude Code version (`claude --version`), OS, and steps to reproduce.

---

> **Still have questions?** Check the official docs at [docs.anthropic.com](https://docs.anthropic.com) or ask in the Anthropic Discord community.
