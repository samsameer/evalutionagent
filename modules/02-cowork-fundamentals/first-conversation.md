# Lesson 3: Your First Conversation

**Module 02, Lesson 3 | Claude Cowork Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

You have configured the app and granted folder access. Now it is time to have your first productive conversation with Claude Cowork. This lesson teaches you how to write effective instructions, walks you through example tasks, and helps you understand how Claude communicates and confirms actions.

---

## 1. How to Write Effective Instructions

Claude Cowork works best when your instructions are clear, specific, and direct. Think of it like giving directions to a capable assistant who is new to your project.

### The 4 Principles of Good Instructions

**Be Specific**
- Weak: *"Make a document."*
- Strong: *"Create a file called meeting-notes.txt in my project-a folder with today's date as the title."*

**State the Goal**
- Weak: *"Fix this file."*
- Strong: *"Review the file report.txt and correct any spelling errors."*

**Provide Context**
- Weak: *"Organise my files."*
- Strong: *"In my project-a folder, move all .pdf files into a subfolder called reports."*

**One Task at a Time (When Starting Out)**
- Start with single, focused requests. As you gain confidence, you can give Claude multi-step instructions.

### Helpful Phrases to Use

- *"In the folder [folder name], please..."*
- *"Create a new file called [filename] with the following content..."*
- *"List all files in [folder name] and tell me what each one contains."*
- *"Read [filename] and summarise the key points."*

### State Your Preferences

If you have a preferred format, tone, or structure, say so upfront:

> *"Use bullet points, keep language simple, and limit the document to one page."*

---

## 2. Example First Tasks

Try these beginner-friendly tasks to get comfortable with Cowork. Make sure you have granted Claude access to your work folder before starting.

### Task A: List Files in Your Work Folder

**What to type:**
> *"Please list all the files in my Claude-Projects folder and briefly describe each one."*

**What Claude will do:**
1. Read the contents of your shared folder.
2. Return a list of filenames with short descriptions based on file names and types.

**What you will learn:** How Claude reads your folder and presents information back to you.

---

### Task B: Create a Simple Document

**What to type:**
> *"Create a new file called hello-cowork.txt in my Claude-Projects/scratch folder. The file should contain a short welcome message and today's date."*

**What Claude will do:**
1. Display a confirmation prompt: *"I will create the file hello-cowork.txt in your scratch folder with the following content. Shall I proceed?"*
2. Show you a preview of the file content.
3. Wait for your approval before writing the file.

**What you will learn:** How the action confirmation flow works and how Claude asks for permission before writing files.

---

### Task C: Read and Summarise a File

**What to type (after completing Task B):**
> *"Read the file hello-cowork.txt in my Claude-Projects/scratch folder and tell me what it contains."*

**What Claude will do:**
1. Open and read the file.
2. Present a summary of its contents in the conversation.

**What you will learn:** How Claude processes file contents and reports back to you.

---

## 3. Understanding Cowork's Responses and Action Confirmations

### Response Types

Claude's responses generally fall into three categories:

| Type | Description | Example |
|------|-------------|---------|
| **Informational** | Claude shares information or answers a question. No action is taken on your files. | "Your folder contains 3 files and 1 sub-folder." |
| **Action Proposal** | Claude describes an action it wants to take and asks for your approval. | "I will create report.txt with the following content. Proceed?" |
| **Completion Report** | Claude confirms that an approved action has been carried out. | "Done. The file report.txt has been created in project-a." |

### The Confirmation Flow

When Claude proposes an action, it follows a predictable pattern:

1. **Acknowledgment** — Claude restates what it understands you want.
2. **Action Plan** — Claude describes exactly what it is about to do.
3. **Confirmation Request** — If confirmations are enabled, Claude asks: *"Shall I proceed?"*
4. **Execution** — After you approve, Claude performs the action.
5. **Result Report** — Claude confirms what was done and shows you the outcome.

### Example Conversation Flow

> **You:** Create a file called notes.txt in project-a with the text "Meeting at 3pm tomorrow."
>
> **Claude:** I will create a new file called `notes.txt` in your `project-a` folder with the content "Meeting at 3pm tomorrow." Shall I proceed?
>
> **You:** Yes.
>
> **Claude:** Done. I have created `notes.txt` in `project-a` with the following content:
> ```
> Meeting at 3pm tomorrow.
> ```

### How to Respond to Confirmations

- **Approve:** Click **Allow** or type "Yes" to let Claude proceed.
- **Reject:** Click **Deny** or type "No" / "Cancel" to stop the action.
- **Correct:** Type a correction if something is not quite right (e.g., *"Change the file name to notes-v2.txt instead"*).

> **Important:** Never approve an action you do not fully understand. It is always safe to ask Claude to explain what it plans to do before you allow it.

---

## 4. Common First-Timer Mistakes

Learn from these so you do not have to make them yourself:

### Mistake 1: Being Too Vague

- *"Help me with my files"* gives Claude no actionable direction.
- **Fix:** Specify which files, which folder, and what you want done.

### Mistake 2: Forgetting to Grant Folder Access

- If Claude says it cannot access a folder, revisit [Lesson 2: Folder Access](folder-access.md) and add the folder to your allowed list.

### Mistake 3: Granting Access to Too Many Folders

- Accidentally sharing your entire home directory "just in case."
- **Fix:** Share only the folders you are actively working in. Use a dedicated work folder.

### Mistake 4: Giving Multiple Complex Tasks at Once

- Starting with *"Reorganise all my documents, create a summary of each, and email the results"* is overwhelming for a first session.
- **Fix:** Break work into single steps. Master one task before combining them.

### Mistake 5: Approving Actions Without Reading Them

- Clicking "Allow" on every prompt without reviewing the details can lead to unintended file changes.
- **Fix:** Take five seconds to read each confirmation before approving. Check file names, paths, and content previews.

### Mistake 6: Not Checking the Output

- Assuming Claude got everything right without verifying.
- **Fix:** Always review created or edited files after Claude finishes. Small errors (wrong date, missing section) are easy to catch early.

---

## 5. Practice Exercises

Complete these exercises to build your confidence. All tasks should be performed inside your `Claude-Projects` folder.

### Exercise 1: Explore Your Workspace

> Open a new Cowork conversation and ask Claude to list the contents of your shared folder. Review the output and confirm it matches what you see in your file explorer.

### Exercise 2: Create a Folder Structure

> Ask Claude to create the following folder structure inside `Claude-Projects`:
> ```
> practice/
>     exercise-01/
>     exercise-02/
>     exercise-03/
> ```
> Verify that the folders were created correctly.

### Exercise 3: Create a Document

> Ask Claude to create a file called `my-goals.txt` inside `practice/exercise-01/` with three professional goals for this year. Review the confirmation prompt carefully before approving.

### Exercise 4: Read and Edit

> Ask Claude to read `my-goals.txt` and add a fourth goal. Pay attention to how Claude handles editing an existing file versus creating a new one.

### Exercise 5: Clean Up and Revoke

> Go to **Settings > Folder Permissions**, remove access to your `Claude-Projects` folder, and then try asking Claude to list files. Observe the permission error. Re-grant access and try again.

---

## Summary

You have now:

- Learned how to write clear, effective instructions for Claude Cowork
- Completed example tasks including listing files, creating documents, and reading content
- Understood how Claude communicates actions and asks for confirmation
- Identified common mistakes and how to avoid them
- Practiced with hands-on exercises

Congratulations — you have completed Module 02! You are ready to move on to Module 03, where you will learn about file management in depth.

---

## Navigation

| | |
|---|---|
| [Back to Module 02 Overview](README.md) | Return to the module page |
| [Previous Lesson: Folder Access](folder-access.md) | Lesson 2 |
| [Next Module: File Management](../03-file-management/) | Module 03 |
| [Back to Course Home](../../README.md) | Return to main course overview |

---

*Claude Cowork Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
