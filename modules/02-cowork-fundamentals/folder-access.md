# Lesson 2: Folder Access

**Module 02, Lesson 2 | Claude Cowork Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Claude Cowork needs access to folders on your computer so it can read, create, and edit files on your behalf. This lesson explains why that access is necessary, walks you through granting it step by step, and covers the security practices you should follow to stay safe.

---

## 1. Why Folder Access Is Needed

Without folder access, Claude can only have text conversations — it cannot interact with your files. Granting access unlocks Cowork's most powerful capabilities:

- **Reading files** — Claude can review documents, spreadsheets, and data files you point it to.
- **Creating files** — Claude can draft reports, generate templates, and produce new documents directly in your folders.
- **Editing files** — Claude can update existing files based on your instructions.
- **Organising files** — Claude can rename, move, and structure files within the folders you share.

Think of it like giving a colleague access to a shared drive: they can only work with what you let them see.

---

## 2. How to Grant Access (Step by Step)

### Method A: Through Settings

#### Step 1: Open Cowork Settings
- Click the **gear icon** in the sidebar and navigate to the **Cowork** or **Agent** tab.

#### Step 2: Find the Folder Access Section
- Look for **"Allowed Folders"**, **"Folder Permissions"**, or a similar label.

#### Step 3: Add a Folder
- Click **"Add Folder"** or **"Browse"**.
- A file picker dialog will appear. Navigate to the folder you want to share.
- Select the folder and confirm.

#### Step 4: Set Permissions
- For each folder, choose the appropriate level:
  - **Read Only** — Claude can view files but cannot change anything.
  - **Read and Write** — Claude can view, create, and edit files.
- Start with **Read and Write** for your dedicated work folder, and **Read Only** for reference folders.

#### Step 5: Confirm and Save
- Review your folder list and click **Save** or **Apply**.
- Claude will now be able to access these folders in your next conversation.

#### Step 6: Verify Access
- Start a new conversation and ask Claude: *"Can you list the files in my work folder?"*
- If Claude returns a file listing, access is working correctly.

### Method B: During a Conversation

1. Start a new conversation and give Claude a task that involves files — for example, *"List all the files in my Projects folder."*
2. Claude will display a permission request prompt: *"Claude Cowork is requesting access to ~/Projects. Allow?"*
3. Review the request and click **Allow** or **Allow (Read Only)**.
4. The folder is added to your Permitted Folders list automatically.

---

## 3. Security Best Practices

### Folders You SHOULD Share

- A **dedicated project folder** (e.g., `~/Documents/Claude-Projects/`)
- Specific **work-in-progress directories** where you want Claude's help
- **Reference folders** containing documents Claude needs to read (use Read Only)
- Tutorial or learning material folders
- Temporary scratch directories for experimentation

### Folders You Should NOT Share

| Folder | Reason |
|--------|--------|
| Your entire home directory (`~/` or `C:\Users\You`) | Too broad — exposes personal files, browser data, and application configs. |
| System folders (`/etc`, `/usr`, `C:\Windows`, `/System`) | Operating system files — no reason for Claude to access these. |
| SSH keys and GPG keys (`~/.ssh`, `~/.gnupg`) | Contains private keys and security credentials. |
| Password manager vaults | Sensitive authentication data. |
| `.env` files or API token directories | Credentials that could be accidentally exposed. |
| Browser profile directories | Cookies, saved passwords, browsing history. |
| Financial or medical records | Sensitive personal data — only share if the specific task requires it. |
| Email or messaging archives | Local mail stores and chat backups often contain private information. |
| Cloud sync root folders (entire Dropbox/OneDrive) | Overly broad — share specific sub-folders instead. |

### General Rules

1. **Share the least amount of access needed.** Only grant access to folders relevant to your current work.
2. **Use a dedicated workspace folder.** Keep Claude's work separate from your personal files.
3. **Review shared folders periodically.** Remove access to folders you no longer need Claude to use.
4. **Never share root or top-level system directories.**

---

## 4. Managing and Revoking Permissions

### Viewing Current Permissions

- Go to **Settings > Cowork > Allowed Folders** to see a list of all folders Claude can access, along with permission levels and the date access was granted.

### Modifying Permissions

- Click on any folder in the list to change it from Read and Write to Read Only, or vice versa.
- Click **Save** to apply the change.

### Revoking Access

1. In the Allowed Folders list, find the folder you want to remove.
2. Click the **Remove** or **X** button next to it.
3. Save your changes.
4. Claude will immediately lose access to that folder in all future conversations. Any ongoing tasks that depend on it will stop and notify you.

### When to Revoke

- When a project is finished and you no longer need Claude's help with those files.
- If you accidentally shared a folder containing sensitive information.
- When reorganising your file structure and moving to a new workspace folder.

### Temporary Access

If you only need Claude to access a folder for a single session:

1. Grant access using Method B (during a conversation).
2. When the conversation ends, go to **Settings > Folder Permissions** and remove the entry.

---

## 5. Tips: Use Dedicated Work Folders

Setting up a dedicated workspace is one of the simplest and most effective ways to stay organised and secure.

### Recommended Folder Structure

```
~/Documents/Claude-Projects/
    project-a/
    project-b/
    scratch/           <-- for quick experiments
    templates/         <-- reusable document templates
    reference/         <-- read-only reference materials
```

### Why This Works

- **Clear boundaries** — Claude only sees what is inside `Claude-Projects`, nothing else.
- **Easy cleanup** — When a project is done, move or archive its folder.
- **Simple permissions** — Grant Read and Write to `Claude-Projects` once, and you are set for all your work.
- **No accidental exposure** — Personal files, system files, and credentials stay completely separate.
- **Easy to audit** — You always know where Claude-related files live.

### Quick Setup

1. Create the folder: right-click in your Documents directory and select **New Folder**, then name it `Claude-Projects`.
2. Inside it, create subfolders for each project you want Claude's help with.
3. In Claude Desktop settings, add `Claude-Projects` as your shared folder with Read and Write access.
4. You are ready to go.

> **Recommendation:** Create your dedicated work folder now, before moving on to the next lesson. You will use it for your first Cowork conversation.

---

## Summary

You now know how to:

- Grant Claude access to specific folders on your computer
- Choose appropriate permission levels (Read Only vs. Read and Write)
- Follow security best practices to protect sensitive data
- Manage and revoke permissions when needed
- Set up a dedicated workspace folder for safe, organised collaboration

In the next lesson, you will put everything together and have your first real conversation with Claude Cowork.

---

## Navigation

| | |
|---|---|
| [Back to Module 02 Overview](README.md) | Return to the module page |
| [Previous Lesson: Desktop App Setup](desktop-app-setup.md) | Lesson 1 |
| [Next Lesson: First Conversation](first-conversation.md) | Lesson 3 |

---

*Claude Cowork Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
