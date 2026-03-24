# Troubleshooting Guide

**Claude Cowork Mastery — March 2026**
**By Jabbir Basha, Principal AI Engineer**

---

## Installation Issues

### Claude Desktop Won't Install

| Platform | Issue | Solution |
|----------|-------|----------|
| macOS | "App can't be opened" | Go to System Preferences → Security & Privacy → Click "Open Anyway" |
| macOS | Requires newer macOS | Update to macOS 12 (Monterey) or later |
| Windows | Installer blocked | Right-click installer → Properties → Unblock → Run as Administrator |
| Windows | Missing dependencies | Install the latest Visual C++ Redistributable from Microsoft |

### App Won't Launch

1. Restart your computer
2. Check if another instance is already running (check Task Manager / Activity Monitor)
3. Reinstall the application from the official download page
4. Clear app cache (see platform-specific instructions below)

**macOS cache clear:**
```
Close Claude Desktop
Open Finder → Go → Go to Folder → ~/Library/Application Support/Claude/
Delete the Cache folder
Relaunch Claude Desktop
```

**Windows cache clear:**
```
Close Claude Desktop
Open File Explorer → %AppData%/Claude/
Delete the Cache folder
Relaunch Claude Desktop
```

---

## Account & Subscription Issues

### "Cowork Not Available"

1. **Verify subscription:** Log into claude.ai → Settings → Subscription → Confirm Pro/Team/Enterprise
2. **Update the app:** Check for updates in Claude Desktop → Help → Check for Updates
3. **Re-authenticate:** Sign out → Sign back in → Restart the app
4. **Check rollout status:** Cowork may be rolling out gradually — check Anthropic's blog or status page

### "Session Expired"

- Sign out and sign back in
- Check your internet connection
- Verify your subscription is active (not expired or payment failed)

---

## File Access Issues

### Cowork Can't See My Files

| Issue | Solution |
|-------|----------|
| Folder not granted access | Settings → Folder Access → Add the folder |
| Subfolder access | Granting access to a parent folder includes all subfolders |
| File in use | Close the file in other applications first |
| Permission denied | Check your OS file permissions (right-click → Properties/Get Info) |
| Network drive | Cowork may not access network/mapped drives — copy files locally |

### Cowork Created Files in the Wrong Location

- Use **absolute paths** in your prompts: `Documents/Business/Invoices/` instead of just `Invoices/`
- Verify which folder Cowork considers the "root" in Settings → Folder Access
- Test with a small task first to confirm the path

### Files Are Corrupted or Incorrectly Formatted

- Check the original file isn't corrupted before processing
- For spreadsheets, open the output in a compatible application (Excel, Google Sheets, LibreOffice)
- Try specifying the output format explicitly: "Save as .xlsx format compatible with Microsoft Excel"

---

## Task Execution Issues

### Cowork Stops Mid-Task

**Possible causes:**
- Task hit a usage limit — try again later or simplify the task
- Internet connection dropped (for web research tasks)
- The task is too complex for a single instruction

**Solutions:**
1. Break the task into smaller steps
2. Check your internet connection
3. Verify you haven't hit your subscription's usage limit
4. Retry with a simpler version of the prompt

### Cowork Misunderstands My Instructions

**Tips for clearer prompts:**
- Be specific: "Sort by file type" not "organize these"
- Use numbered steps: "1. Read the PDFs. 2. Extract dates. 3. Create spreadsheet."
- Provide examples: "Use this naming format: 2026-03-15_VendorName_Invoice.pdf"
- Set boundaries: "Only process PDF files. Ignore everything else."

### Web Research Returns Outdated Information

- Specify the time frame: "Find articles from the last 30 days"
- Ask for source dates: "Include the publication date for each source"
- Cross-reference: "Verify pricing information from at least 2 sources"

### Automation Runs But Produces Empty Results

- Check that the source folder contains files
- Verify file formats match what you specified
- Ensure Cowork has access to both source and destination folders
- Run the task manually (not scheduled) first to verify it works

---

## Performance Issues

### Cowork Is Running Slowly

1. Close unnecessary applications to free up memory
2. Reduce the number of files being processed at once
3. Break large tasks into batches (e.g., process 50 files at a time instead of 500)
4. Check your internet speed (affects web research tasks)

### High Memory or CPU Usage

- Claude Desktop processes run locally and may use significant resources during heavy tasks
- Close the app when not in use
- If persistent, reinstall the application

---

## Common Error Messages

| Error | Meaning | Fix |
|-------|---------|-----|
| "Folder access denied" | Claude doesn't have permission to this folder | Add folder in Settings → Folder Access |
| "File not found" | The specified file doesn't exist at that path | Check the file path and spelling |
| "Rate limit exceeded" | You've hit your subscription's usage limit | Wait and try again, or upgrade your plan |
| "Task cancelled" | The task was stopped before completion | Retry with a simpler prompt or check for errors |
| "Unable to read file" | File format not supported or file is corrupted | Try converting to a supported format (PDF, TXT, XLSX) |
| "Network error" | Internet connection issue | Check your connection and retry |

---

## Getting Help

If none of the above solutions work:

1. **Check the [FAQ](faq.md)** for common questions
2. **Visit Anthropic's support page** — see [Links](links.md)
3. **Search Anthropic's community forums** for similar issues
4. **Contact Anthropic support** through your account dashboard

---

[← Back to Resources](README.md) | [Back to Course Home](../README.md)
