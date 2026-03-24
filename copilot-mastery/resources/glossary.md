# Glossary — GitHub Copilot Terminology

**GitHub Copilot Mastery — March 2026**

---

| Term | Definition |
|------|-----------|
| **Agent Mode** | A Copilot Chat mode where the AI autonomously plans, edits files, runs terminal commands, and iterates until a task is complete |
| **Chat Participant** | A scoped domain accessed via `@` syntax in Copilot Chat (e.g., `@workspace`, `@terminal`, `@vscode`) |
| **Code Completion** | Inline code suggestions that appear as ghost text while you type |
| **Code Referencing** | A feature that detects when Copilot suggestions match publicly available code and shows the source and license |
| **Content Exclusion** | Organization policy that prevents specific files or repositories from being sent to Copilot |
| **Context Variable** | A `#` prefixed reference in Copilot Chat that provides specific context (e.g., `#file`, `#selection`, `#codebase`) |
| **Copilot Chat** | The conversational AI interface for asking questions, requesting code changes, and getting explanations |
| **Copilot CLI** | Terminal-based AI assistant accessed via `gh copilot` for explaining and suggesting shell commands |
| **Copilot Coding Agent** | An autonomous AI that can be assigned GitHub Issues and independently creates pull requests to resolve them |
| **Copilot Edits** | A multi-file editing mode where Copilot proposes changes across multiple files with diff review |
| **Copilot Extension** | A third-party plugin that adds new capabilities to Copilot Chat (e.g., `@docker`, `@sentry`) |
| **Copilot Workspace** | A cloud-based development environment on GitHub.com for going from an issue to a pull request |
| **Custom Instructions** | Project-specific rules defined in `.github/copilot-instructions.md` that shape Copilot's behavior |
| **FIM (Fill-in-the-Middle)** | A completion technique where Copilot suggests code to fill between existing code, not just at the end |
| **Ghost Text** | Semi-transparent code suggestions that appear inline in your editor |
| **Inline Chat** | A Copilot Chat interface that appears directly in the editor at the cursor position (`Ctrl+I`) |
| **IP Indemnity** | Legal protection provided by GitHub for Business/Enterprise customers against IP infringement claims from AI-generated code |
| **Knowledge Base** | A curated collection of documentation repositories that Copilot Enterprise uses as additional context |
| **LLM (Large Language Model)** | The AI model (like GPT-4o, Claude, Gemini) that powers Copilot's code generation and chat |
| **MCP (Model Context Protocol)** | An open standard for connecting AI models to external tools and data sources |
| **MCP Server** | A process that exposes tools, resources, and prompts via the Model Context Protocol |
| **NES (Next Edit Suggestions)** | A feature that predicts where you need to edit next after making a change and offers the related modification |
| **Partial Accept** | Accepting a suggestion word-by-word (`Ctrl+Right Arrow`) instead of all at once |
| **Premium Request** | An interaction that uses advanced models (o1, o3-mini) or agentic features, counted against a monthly allowance |
| **Prompt File** | A reusable prompt template stored in `.github/prompts/*.prompt.md` that can be invoked in Copilot Chat |
| **Public Code Filter** | A setting that controls whether suggestions matching public code are shown, blocked, or flagged |
| **Quick Chat** | A lightweight, floating Copilot Chat dialog for fast questions (`Ctrl+Shift+I`) |
| **Slash Command** | A `/` prefixed command in Copilot Chat that triggers specific actions (e.g., `/explain`, `/fix`, `/tests`) |
| **Working Set** | The collection of files that Copilot Edits is allowed to modify during an editing session |

---

[← Back to Course Home](../README.md)

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
