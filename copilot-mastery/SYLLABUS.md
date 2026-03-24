# Course Syllabus: GitHub Copilot Mastery

**Instructor:** Jabbir Basha, Principal AI Engineer
**Edition:** March 2026
**Duration:** Self-paced (12 Modules)
**Difficulty:** Beginner to Expert — Covers all levels

---

## Module 01: Introduction to GitHub Copilot

**Learning Objectives:**
- Understand what GitHub Copilot is and the AI models powering it
- Learn about all Copilot plans (Free, Pro, Pro+, Business, Enterprise) and their features
- Understand how Copilot generates code suggestions using LLMs and context

**Lessons:**
1. [What is GitHub Copilot?](modules/01-introduction/README.md)
2. [Plans, Pricing & Feature Comparison](modules/01-introduction/plans-and-pricing.md)
3. [How Copilot Works Under the Hood](modules/01-introduction/how-copilot-works.md)

---

## Module 02: Setup & Installation

**Learning Objectives:**
- Install and configure GitHub Copilot in VS Code, JetBrains, Neovim, and Xcode
- Set up Copilot CLI in your terminal
- Configure authentication and verify Copilot is active

**Lessons:**
1. [Module Overview](modules/02-setup-installation/README.md)
2. [VS Code Setup](modules/02-setup-installation/vs-code-setup.md)
3. [JetBrains IDE Setup](modules/02-setup-installation/jetbrains-setup.md)
4. [Neovim & Xcode Setup](modules/02-setup-installation/neovim-xcode-setup.md)
5. [Copilot CLI Installation](modules/02-setup-installation/cli-installation.md)

---

## Module 03: Copilot in VS Code — Core Features

**Learning Objectives:**
- Master inline code completions and ghost text suggestions
- Use tab to accept, partial accept, and navigate between suggestions
- Understand and leverage Next Edit Suggestions (NES)
- Work with multi-line and function-level completions

**Lessons:**
1. [Module Overview](modules/03-vs-code-core/README.md)
2. [Inline Completions & Ghost Text](modules/03-vs-code-core/inline-completions.md)
3. [Next Edit Suggestions (NES)](modules/03-vs-code-core/next-edit-suggestions.md)
4. [Completions Panel & Navigation](modules/03-vs-code-core/completions-panel.md)

---

## Module 04: Copilot Chat Deep Dive

**Learning Objectives:**
- Master Copilot Chat in VS Code — inline chat, chat panel, and quick chat
- Use chat participants (@workspace, @terminal, @vscode, @github)
- Leverage slash commands (/explain, /fix, /tests, /doc, /new, /optimize)
- Use context variables (#file, #selection, #editor, #codebase, #terminalLastCommand)
- Utilize vision capabilities to ask about images and screenshots

**Lessons:**
1. [Module Overview](modules/04-copilot-chat/README.md)
2. [Chat Modes — Inline, Panel & Quick Chat](modules/04-copilot-chat/chat-modes.md)
3. [Chat Participants & Slash Commands](modules/04-copilot-chat/participants-and-commands.md)
4. [Context Variables & References](modules/04-copilot-chat/context-variables.md)
5. [Vision & Image Understanding](modules/04-copilot-chat/vision-capabilities.md)

---

## Module 05: Copilot Edits & Agent Mode

**Learning Objectives:**
- Use Copilot Edits for multi-file editing sessions
- Master Agent Mode for autonomous multi-step task execution
- Understand how agent mode runs terminal commands, installs packages, and fixes errors
- Configure MCP servers for agent mode tool access

**Lessons:**
1. [Module Overview](modules/05-copilot-edits-agent-mode/README.md)
2. [Copilot Edits — Multi-File Editing](modules/05-copilot-edits-agent-mode/copilot-edits.md)
3. [Agent Mode — Autonomous Coding](modules/05-copilot-edits-agent-mode/agent-mode.md)
4. [MCP Tools in Agent Mode](modules/05-copilot-edits-agent-mode/mcp-tools.md)

---

## Module 06: GitHub Copilot CLI

**Learning Objectives:**
- Install and authenticate the GitHub Copilot CLI extension
- Use `gh copilot explain` to understand complex shell commands
- Use `gh copilot suggest` to generate commands for shell, Git, and GitHub CLI
- Integrate Copilot CLI into daily terminal workflows

**Lessons:**
1. [Module Overview](modules/06-copilot-cli/README.md)
2. [Installation & Authentication](modules/06-copilot-cli/installation.md)
3. [Explain Commands](modules/06-copilot-cli/explain-commands.md)
4. [Suggest Commands](modules/06-copilot-cli/suggest-commands.md)
5. [Advanced CLI Workflows](modules/06-copilot-cli/advanced-workflows.md)

---

## Module 07: Copilot on GitHub.com

**Learning Objectives:**
- Use Copilot Chat on github.com for repository-level questions
- Generate AI-powered PR summaries and descriptions
- Leverage Copilot for code review assistance
- Understand Copilot Workspace for issue-to-PR workflows

**Lessons:**
1. [Module Overview](modules/07-github-dot-com/README.md)
2. [Copilot Chat on GitHub.com](modules/07-github-dot-com/copilot-chat-web.md)
3. [AI-Powered Pull Request Summaries](modules/07-github-dot-com/pr-summaries.md)
4. [Copilot Code Review](modules/07-github-dot-com/code-review.md)
5. [Copilot Workspace](modules/07-github-dot-com/copilot-workspace.md)

---

## Module 08: Copilot Coding Agent

**Learning Objectives:**
- Understand the Copilot Coding Agent and its autonomous capabilities
- Assign GitHub Issues to Copilot for automatic resolution
- Review agent-created pull requests and provide feedback
- Configure agent permissions, firewalls, and allowed tools

**Lessons:**
1. [Module Overview](modules/08-coding-agent/README.md)
2. [What is the Coding Agent?](modules/08-coding-agent/what-is-coding-agent.md)
3. [Assigning Issues to Copilot](modules/08-coding-agent/assigning-issues.md)
4. [Reviewing Agent Pull Requests](modules/08-coding-agent/reviewing-agent-prs.md)
5. [Agent Configuration & Permissions](modules/08-coding-agent/agent-configuration.md)

---

## Module 09: Extensions & MCP

**Learning Objectives:**
- Understand Copilot Extensions and how they expand functionality
- Learn about the Model Context Protocol (MCP) and its role in Copilot
- Configure MCP servers for VS Code and agent mode
- Discover popular extensions and third-party integrations

**Lessons:**
1. [Module Overview](modules/09-extensions-mcp/README.md)
2. [Copilot Extensions Marketplace](modules/09-extensions-mcp/extensions-marketplace.md)
3. [Model Context Protocol (MCP) Explained](modules/09-extensions-mcp/mcp-explained.md)
4. [Configuring MCP Servers](modules/09-extensions-mcp/configuring-mcp-servers.md)
5. [Building Custom Extensions](modules/09-extensions-mcp/building-extensions.md)

---

## Module 10: Advanced Features & Custom Instructions

**Learning Objectives:**
- Create custom instructions with `.github/copilot-instructions.md`
- Select and switch between AI models (GPT-4o, Claude, Gemini, o1, o3-mini)
- Use prompt files (`.github/prompts/*.prompt.md`) for reusable workflows
- Configure knowledge bases for Enterprise deployments
- Master prompt engineering for optimal Copilot responses

**Lessons:**
1. [Module Overview](modules/10-advanced-features/README.md)
2. [Custom Instructions](modules/10-advanced-features/custom-instructions.md)
3. [Model Selection & Switching](modules/10-advanced-features/model-selection.md)
4. [Prompt Files & Reusable Prompts](modules/10-advanced-features/prompt-files.md)
5. [Knowledge Bases (Enterprise)](modules/10-advanced-features/knowledge-bases.md)
6. [Prompt Engineering for Copilot](modules/10-advanced-features/prompt-engineering.md)

---

## Module 11: Security, Privacy & Admin

**Learning Objectives:**
- Understand Copilot's data privacy model and what code is sent/stored
- Configure content exclusions to prevent sensitive files from being processed
- Manage organization-wide policies and seat assignments
- Understand IP indemnity, code referencing, and public code matching
- Use Copilot metrics and usage analytics

**Lessons:**
1. [Module Overview](modules/11-security-privacy-admin/README.md)
2. [Data Privacy & Code Handling](modules/11-security-privacy-admin/data-privacy.md)
3. [Content Exclusions](modules/11-security-privacy-admin/content-exclusions.md)
4. [Organization Policies & Seat Management](modules/11-security-privacy-admin/org-policies.md)
5. [IP Indemnity & Code Referencing](modules/11-security-privacy-admin/ip-indemnity.md)
6. [Metrics & Usage Analytics](modules/11-security-privacy-admin/metrics-analytics.md)

---

## Module 12: Real-World Projects & Workflows

**Learning Objectives:**
- Build a full-stack web application with Copilot from scratch
- Create a complete REST API with tests using agent mode
- Set up a CI/CD pipeline with Copilot assistance
- Implement team workflows and code review practices with Copilot

**Lessons:**
1. [Module Overview](modules/12-real-world-projects/README.md)
2. [Building a Full-Stack App with Agent Mode](modules/12-real-world-projects/fullstack-app.md)
3. [REST API with Tests](modules/12-real-world-projects/rest-api-tests.md)
4. [CI/CD Pipeline Setup](modules/12-real-world-projects/cicd-pipeline.md)
5. [Team Workflows & Best Practices](modules/12-real-world-projects/team-workflows.md)

---

## Supplementary Materials

- [Prompt Templates](templates/prompt-templates.md) — Copy-paste prompts for common Copilot tasks
- [Custom Instructions Examples](templates/copilot-instructions-examples.md) — Ready-to-use `.github/copilot-instructions.md` files
- [Workflow Recipes](templates/workflow-recipes.md) — Step-by-step recipes for common development workflows
- [Keyboard Shortcuts](resources/keyboard-shortcuts.md) — Complete shortcut reference for all platforms
- [Glossary](resources/glossary.md) — AI and Copilot terminology
- [FAQ](resources/faq.md) — Frequently asked questions
- [Troubleshooting](resources/troubleshooting.md) — Common issues and solutions
- [Links & References](resources/links.md) — Official GitHub and Copilot resources

---

*Course by Jabbir Basha, Principal AI Engineer — March 2026*
