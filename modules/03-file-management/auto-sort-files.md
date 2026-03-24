# Module 03, Lesson 1 | Claude Cowork Mastery — March 2026

**Instructor:** Jabbir Basha, Principal AI Engineer

---

# Auto-Sorting Files with Claude Cowork

Sorting files manually is one of the most common time sinks in daily computer use. Whether it is a cluttered Downloads folder or a shared drive full of mixed documents, Claude Cowork can sort everything for you in seconds.

---

## What You Will Learn

- How to set up a source folder for sorting
- How Cowork identifies file types and creates categories
- How to sort by date, project, file type, or client
- Practical prompts you can copy and use immediately

---

## Step 1: Setting Up a Source Folder

Before asking Cowork to sort your files, identify the folder you want to organize. This is your **source folder** — the directory where unsorted files currently live.

Common examples of source folders:

- Your **Downloads** folder
- A **Desktop** cluttered with files
- A shared **Documents** folder with mixed content
- An **Inbox** folder where clients send files

Make sure you know the exact path to this folder. For example:
- Windows: `C:\Users\YourName\Downloads`
- Mac: `/Users/YourName/Downloads`

---

## Step 2: Ask Cowork to Sort Your Files

The simplest way to get started is with a direct prompt. Open Claude Cowork and type:

> **"Sort all files in my Downloads folder by type."**

Cowork will:

1. Scan the folder and identify every file
2. Detect each file's type (PDF, image, spreadsheet, document, etc.)
3. Create category folders (e.g., `PDFs`, `Images`, `Spreadsheets`, `Documents`)
4. Move each file into the appropriate folder

---

## Step 3: How Cowork Identifies File Types

Claude Cowork recognizes files by their extensions and content. Here is how it categorizes common files:

| Category | File Types |
|----------|-----------|
| Documents | .docx, .doc, .txt, .rtf, .odt |
| Spreadsheets | .xlsx, .xls, .csv, .ods |
| PDFs | .pdf |
| Images | .jpg, .jpeg, .png, .gif, .svg, .webp |
| Videos | .mp4, .mov, .avi, .mkv |
| Audio | .mp3, .wav, .aac, .flac |
| Archives | .zip, .rar, .7z, .tar.gz |
| Presentations | .pptx, .ppt, .key |

---

## Step 4: Sorting by Different Criteria

You are not limited to sorting by file type. Cowork can sort by several criteria depending on your needs.

### Sort by Date

> **"Sort all files in my Documents folder into subfolders by month and year."**

This creates a structure like:

```
Documents/
  2025-11/
  2025-12/
  2026-01/
  2026-02/
  2026-03/
```

### Sort by Project

> **"Sort files in my Work folder into subfolders based on project name found in the filename."**

### Sort by Client

> **"Organize all invoices by client name. Group files that mention the same company into one folder."**

---

## Real-World Example: Sorting Invoices and Bank Statements

Imagine you have a folder called `Financial_Docs` with the following files mixed together:

```
Financial_Docs/
  invoice-acme-jan2026.pdf
  bank-statement-feb2026.pdf
  invoice-globex-feb2026.pdf
  receipt-office-supplies.pdf
  bank-statement-jan2026.pdf
  invoice-acme-feb2026.pdf
  tax-form-2025.pdf
```

You open Claude Cowork and type:

> **"Sort all files in my Financial_Docs folder. Separate invoices, bank statements, receipts, and tax documents into their own folders."**

Cowork produces:

```
Financial_Docs/
  Invoices/
    invoice-acme-jan2026.pdf
    invoice-acme-feb2026.pdf
    invoice-globex-feb2026.pdf
  Bank_Statements/
    bank-statement-jan2026.pdf
    bank-statement-feb2026.pdf
  Receipts/
    receipt-office-supplies.pdf
  Tax_Documents/
    tax-form-2025.pdf
```

Clean, organized, and done in seconds.

---

## Sample Prompts You Can Copy and Paste

Use any of these prompts directly in Claude Cowork:

1. **Basic sort by type:**
   > "Sort all files in my Downloads folder by file type into separate subfolders."

2. **Sort by date:**
   > "Organize my Documents folder by grouping files into monthly subfolders based on their last modified date."

3. **Sort by client:**
   > "Group all files in my Clients folder by client name. Use the first word of each filename as the client name."

4. **Sort mixed media:**
   > "Separate images, videos, and documents in my Desktop folder into their own subfolders."

5. **Sort with nested structure:**
   > "Sort my Project_Files folder first by project name, then by file type within each project."

---

## Tips for Best Results

- **Be specific** about the folder path so Cowork knows exactly where to look
- **Describe the sorting logic** you want — Cowork follows your instructions precisely
- **Ask for a preview first** if you are unsure: "Show me how you would sort these files before moving them."
- **Always back up first** if the folder contains important files (see [Lesson 3: Backup Strategies](backup-strategies.md))

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 03: Automated File Management](README.md) |
| Next Lesson | [Lesson 2: Rename & Organize](rename-organize.md) |

---

*Claude Cowork Mastery — March 2026*
