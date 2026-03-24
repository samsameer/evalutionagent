# Frequently Asked Questions

**GitHub Copilot Mastery — March 2026**

---

## General

### Is GitHub Copilot free?

Yes, there is a **free tier** with 2,000 code completions and 50 chat messages per month. For unlimited access and advanced features, you need a paid plan starting at $10/month (Pro).

### Does Copilot work offline?

No. Copilot requires an internet connection to communicate with AI models hosted on GitHub's servers. There is no offline mode.

### What programming languages does Copilot support?

Copilot works with virtually every programming language. It is strongest in Python, JavaScript, TypeScript, Java, C#, Go, and Rust, but also works well with Ruby, PHP, Swift, Kotlin, C++, and many others.

### Does Copilot write perfect code?

No. Copilot is a powerful assistant, but its suggestions should always be reviewed. It can introduce bugs, security vulnerabilities, or suboptimal patterns. Treat AI-generated code with the same scrutiny as code from a junior developer.

---

## Privacy & Security

### Does GitHub use my code to train AI models?

No. As of 2024, GitHub does not use your code to train models (opt-out is the default for all plans). Business and Enterprise plans have the strongest guarantee — code is never retained.

### Is my code sent to the cloud?

Yes. Code context (snippets from your current file and open tabs) is sent to GitHub's servers for processing. It is encrypted in transit (TLS 1.2+) and not stored after the suggestion is generated.

### Can I prevent sensitive files from being processed?

Yes, if you have a Business or Enterprise plan. Use **content exclusions** to specify files, directories, or repositories that Copilot should never process. See [Module 11: Content Exclusions](../modules/11-security-privacy-admin/content-exclusions.md).

---

## Features

### What is Agent Mode?

Agent mode is a Copilot Chat mode where the AI autonomously plans, writes code across multiple files, runs terminal commands, reads output, and self-corrects — all from a single natural language instruction. See [Module 05](../modules/05-copilot-edits-agent-mode/agent-mode.md).

### What is the Copilot Coding Agent?

The coding agent is a fully autonomous AI developer that you can assign GitHub Issues to. It creates a branch, writes code, runs tests, and opens a pull request — all in the background. Available on Pro+ and Enterprise plans. See [Module 08](../modules/08-coding-agent/).

### What is MCP?

MCP (Model Context Protocol) is an open standard that lets Copilot agent mode connect to external tools like databases, APIs, and cloud services. See [Module 09](../modules/09-extensions-mcp/mcp-explained.md).

### What are Next Edit Suggestions (NES)?

NES predicts where you need to edit next after making a change and offers the related modification. For example, if you rename a parameter, NES suggests updating all references. See [Module 03](../modules/03-vs-code-core/next-edit-suggestions.md).

---

## Plans & Pricing

### Which plan should I choose?

- **Free**: Hobby projects, students, trying Copilot
- **Pro ($10/mo)**: Professional developers, daily coding
- **Pro+ ($39/mo)**: Power users who want the coding agent and premium models
- **Business ($19/user/mo)**: Teams needing IP indemnity and admin controls
- **Enterprise ($39/user/mo)**: Large organizations needing everything

See [Module 01: Plans & Pricing](../modules/01-introduction/plans-and-pricing.md) for a detailed comparison.

### Do students get Copilot for free?

Yes. Verified students and educators get free Copilot Pro access through the GitHub Education program.

---

## Troubleshooting

### Copilot is not showing suggestions

1. Check that the Copilot extension is installed and enabled
2. Verify you are signed in (`Copilot` status bar icon)
3. Check that the file type is not disabled in settings
4. Ensure your subscription is active
5. Try reloading VS Code

### Copilot Chat is not responding

1. Check your internet connection
2. Verify the Copilot Chat extension is installed
3. Try switching to a different AI model
4. Reload VS Code window

See [Troubleshooting Guide](troubleshooting.md) for more solutions.

---

[← Back to Course Home](../README.md)

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
