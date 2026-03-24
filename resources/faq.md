# Frequently Asked Questions

**Claude Cowork Mastery — March 2026**
**By Jabbir Basha, Principal AI Engineer**

---

## General Questions

### Q: Is Claude Cowork free?
**No.** Claude Cowork requires a paid subscription. You need at least a **Claude Pro** plan. Team and Enterprise plans also include Cowork access. The free tier of Claude does NOT include Cowork.

### Q: What's the difference between Claude (the chatbot) and Claude Cowork?
Regular Claude is a conversational AI — you ask questions, it gives text answers. **Cowork is an agent** — you give it tasks, and it actually performs them. It can access your files, browse the web, create spreadsheets, and execute multi-step workflows.

### Q: Do I need to know how to code?
**Absolutely not.** This entire course is designed for non-technical users. If you can type a message and organize files in folders, you have all the skills you need.

### Q: What operating systems are supported?
Claude Desktop (required for Cowork) is available for **macOS** and **Windows**. Linux is not officially supported as of March 2026.

### Q: Is my data safe with Cowork?
Anthropic takes data security seriously. Cowork only accesses folders you explicitly grant permission to. Your files are processed locally through the desktop app, and you can revoke access at any time. Review Anthropic's privacy policy for full details.

---

## Setup & Access

### Q: I have a Pro subscription but can't see Cowork. What do I do?
1. Make sure your Claude Desktop app is updated to the latest version
2. Sign out and sign back in
3. Check Anthropic's status page for any rollout updates
4. Restart the application
5. If still not working, contact Anthropic support

### Q: Can I use Cowork in the web browser (claude.ai)?
Cowork's full capabilities (file access, local automation) require the **Claude Desktop app**. Some features may be available in the web interface, but for the full experience covered in this course, use the desktop app.

### Q: How do I grant folder access?
In Claude Desktop, go to **Settings → Folder Access** and add the folders you want Cowork to access. See [Module 02: Folder Access](../modules/02-cowork-fundamentals/folder-access.md) for a detailed walkthrough.

### Q: Which folders should I share with Cowork?
Share **work folders** that contain the documents, invoices, or data you want Cowork to process. **Do NOT share** folders containing passwords, credentials, personal medical records, or other sensitive information. See our [Folder Structures](../templates/folder-structures.md) for recommended setups.

---

## Using Cowork

### Q: What happens if Cowork makes a mistake with my files?
Always create backups before running automation on important files. You can also ask Cowork to create a backup first: "Before making any changes, create a copy of the entire folder." See [Module 03: Backup Strategies](../modules/03-file-management/backup-strategies.md).

### Q: Can Cowork delete my files?
Cowork can delete files if instructed to, but it typically asks for confirmation before destructive actions. Best practice: always include "Do NOT delete any files" in your prompts unless deletion is specifically what you want.

### Q: How large of files can Cowork handle?
Cowork can process most standard business documents (PDFs, spreadsheets, text files). Very large files (hundreds of megabytes) may take longer or require breaking into smaller pieces. Check Anthropic's documentation for current size limits.

### Q: Can Cowork work with Google Docs or cloud files?
Cowork primarily works with files on your local computer. For cloud files, download them to a local folder first, then let Cowork process them. Some MCP integrations may enable direct cloud access — check Anthropic's latest updates.

### Q: What file formats does Cowork support?
Common supported formats include:
- Documents: PDF, TXT, DOCX, MD
- Spreadsheets: XLSX, CSV
- Images: JPG, PNG (for receipt scanning)
- Data: JSON, XML

---

## Troubleshooting

### Q: Cowork seems to be "stuck" on a task. What should I do?
1. Wait a moment — complex tasks may take time
2. Check if Cowork is asking for clarification (scroll up in the chat)
3. If truly stuck, you can cancel the current task and try again with a simpler prompt
4. Break large tasks into smaller steps

### Q: The data Cowork extracted from my PDF is incorrect.
- Check the PDF quality — scanned documents with poor quality may produce errors
- Try providing more specific instructions about what to extract
- Verify with a small sample first before processing large batches
- Some PDFs have security restrictions that prevent reading

### Q: My recurring automation didn't run as scheduled.
- Ensure the Claude Desktop app is running (it needs to be open for scheduled tasks)
- Check your internet connection (needed for web research tasks)
- Verify the folder paths in your instructions still exist
- Review the automation settings in Cowork preferences

### Q: Cowork created the wrong folder structure.
- Be more specific in your prompt — use exact paths
- Copy-paste folder structures from our [Templates](../templates/folder-structures.md)
- Ask Cowork to show you what it plans to create before executing

---

## Billing & Subscription

### Q: Can I try Cowork before subscribing?
Check Anthropic's current offerings — they may offer a trial period. As of March 2026, Cowork requires at minimum a Pro subscription.

### Q: What's the difference between Pro, Team, and Enterprise?
- **Pro:** Individual use, full Cowork access, standard usage limits
- **Team:** Multi-user, shared billing, collaboration features
- **Enterprise:** Custom limits, SSO, admin controls, dedicated support

### Q: Will I be charged extra for Cowork?
Cowork is included with your Pro/Team/Enterprise subscription. There are no additional charges for Cowork specifically, but usage counts toward your plan's usage limits.

---

## Still Have Questions?

- Check the [Troubleshooting Guide](troubleshooting.md) for technical issues
- Visit the [Glossary](glossary.md) for term definitions
- See [Official Links](links.md) for Anthropic's support channels

---

[← Back to Resources](README.md) | [Back to Course Home](../README.md)
