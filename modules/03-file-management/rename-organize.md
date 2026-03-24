# Module 03, Lesson 2 | Claude Cowork Mastery — March 2026

**Instructor:** Jabbir Basha, Principal AI Engineer

---

# Batch Renaming and Organization

Inconsistent filenames make it harder to find what you need, cause confusion in shared folders, and create headaches during audits or reviews. In this lesson, you will learn how to use Claude Cowork to rename files in bulk and organize them into clean, structured folders.

---

## What You Will Learn

- Why consistent naming matters
- Common naming convention patterns
- How to batch rename files with a single prompt
- How to organize files into project-based folder structures
- Before-and-after examples to see the transformation

---

## Why Consistent Naming Matters

Consider these two versions of the same folder:

**Without naming conventions:**
```
scan0042.pdf
Invoice_FINAL_v2.pdf
john - invoice feb.pdf
INV-Feb2026.pdf
invoice(1).pdf
```

**With naming conventions:**
```
2026-01-AcmeCorp-Invoice.pdf
2026-02-AcmeCorp-Invoice.pdf
2026-02-GlobexInc-Invoice.pdf
2026-02-WayneEnt-Invoice.pdf
2026-03-AcmeCorp-Invoice.pdf
```

The second version is instantly searchable, sortable, and understandable. Claude Cowork can transform the first into the second with a single prompt.

---

## Naming Convention Examples

Here are three popular naming patterns you can ask Cowork to apply:

### Date-Based Naming

Format: `YYYY-MM-DD-Description.ext`

```
2026-03-15-TeamMeeting-Notes.docx
2026-03-20-QuarterlyReport.xlsx
2026-03-24-ClientProposal.pdf
```

Best for: meeting notes, reports, daily logs, time-sensitive documents.

### Client-Based Naming

Format: `ClientName-DocumentType-Date.ext`

```
AcmeCorp-Invoice-2026-01.pdf
AcmeCorp-Invoice-2026-02.pdf
GlobexInc-Contract-2026-03.pdf
```

Best for: invoices, contracts, client correspondence, project deliverables.

### Project-Based Naming

Format: `ProjectName-Phase-Description.ext`

```
WebsiteRedesign-Phase1-Wireframes.pdf
WebsiteRedesign-Phase2-Mockups.png
WebsiteRedesign-Phase3-FinalDesign.fig
```

Best for: project deliverables, design files, development assets.

---

## Batch Renaming with Claude Cowork

### Basic Rename by Convention

Open Claude Cowork and use this prompt:

> **"Rename all PDFs in my Invoices folder to the format: YYYY-MM-ClientName-Invoice.pdf. Use the content of each file to determine the date and client name."**

Cowork will:

1. Open and read each PDF to extract the date and client name
2. Construct the new filename following your specified format
3. Rename each file accordingly

### Rename with a Prefix

> **"Add the prefix 'ARCHIVED-' to all files in my Old_Projects folder."**

**Before:**
```
ProjectAlpha-Report.pdf
ProjectBeta-Summary.docx
ProjectGamma-Budget.xlsx
```

**After:**
```
ARCHIVED-ProjectAlpha-Report.pdf
ARCHIVED-ProjectBeta-Summary.docx
ARCHIVED-ProjectGamma-Budget.xlsx
```

### Rename by Replacing Text

> **"In my Reports folder, replace all spaces in filenames with hyphens and convert everything to lowercase."**

**Before:**
```
Quarterly Report Q1.pdf
Annual Review 2025.docx
Team Performance Summary.xlsx
```

**After:**
```
quarterly-report-q1.pdf
annual-review-2025.docx
team-performance-summary.xlsx
```

---

## Organizing Files into Project-Based Folder Structures

Beyond renaming, Cowork can restructure entire directories. Here is how to go from a flat, messy folder to a clean project hierarchy.

### Example Prompt

> **"Organize all files in my Work folder into project-based subfolders. Each project should have subfolders for Documents, Spreadsheets, and Images. Determine the project from each filename."**

### Before

```
Work/
  alpha-budget.xlsx
  alpha-proposal.pdf
  alpha-logo.png
  beta-contract.pdf
  beta-timeline.xlsx
  beta-mockup.jpg
  gamma-report.docx
  gamma-data.csv
```

### After

```
Work/
  Alpha/
    Documents/
      alpha-proposal.pdf
    Spreadsheets/
      alpha-budget.xlsx
    Images/
      alpha-logo.png
  Beta/
    Documents/
      beta-contract.pdf
    Spreadsheets/
      beta-timeline.xlsx
    Images/
      beta-mockup.jpg
  Gamma/
    Documents/
      gamma-report.docx
    Spreadsheets/
      gamma-data.csv
```

---

## Before-and-After: Full Workflow Example

**Scenario:** You have a folder of 50 client invoices with inconsistent names accumulated over several months.

**Step 1 — Ask Cowork to preview:**

> "Show me a list of all files in my Invoices folder and suggest a consistent naming format."

**Step 2 — Approve and rename:**

> "Rename all files in my Invoices folder to the format: YYYY-MM-ClientName-Invoice.pdf based on your suggestions."

**Step 3 — Organize by client:**

> "Now move each renamed invoice into a subfolder named after the client."

**Final result:**

```
Invoices/
  AcmeCorp/
    2026-01-AcmeCorp-Invoice.pdf
    2026-02-AcmeCorp-Invoice.pdf
    2026-03-AcmeCorp-Invoice.pdf
  GlobexInc/
    2026-01-GlobexInc-Invoice.pdf
    2026-02-GlobexInc-Invoice.pdf
  WayneEnt/
    2026-03-WayneEnt-Invoice.pdf
```

---

## Sample Prompts You Can Copy and Paste

1. **Date-based rename:**
   > "Rename all files in my Reports folder to start with the date in YYYY-MM-DD format, followed by the original filename."

2. **Client-based rename:**
   > "Rename all PDFs in my Contracts folder to the format: ClientName-Contract-YYYY.pdf."

3. **Remove clutter from filenames:**
   > "Remove all special characters and extra spaces from filenames in my Documents folder. Replace spaces with hyphens."

4. **Number files sequentially:**
   > "Rename all images in my Photos folder to Photo-001.jpg, Photo-002.jpg, etc., in alphabetical order."

5. **Organize into subfolders after renaming:**
   > "After renaming, move all files into subfolders based on the year in their filename."

---

## Tips for Best Results

- **Always preview first** — ask Cowork to show you the proposed changes before executing
- **Be explicit about your format** — the more precise your naming pattern, the better the results
- **Handle duplicates** — tell Cowork what to do if two files would end up with the same name (e.g., append a number)
- **Back up before renaming** — renaming is harder to undo than sorting (see [Lesson 3: Backup Strategies](backup-strategies.md))

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 03: Automated File Management](README.md) |
| Previous Lesson | [Lesson 1: Auto-Sort Files](auto-sort-files.md) |
| Next Lesson | [Lesson 3: Backup Strategies](backup-strategies.md) |

---

*Claude Cowork Mastery — March 2026*
