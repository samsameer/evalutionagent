# Module 04, Lesson 3 | Claude Cowork Mastery — March 2026

## Generating Financial Reports

**Instructor:** Jabbir Basha, Principal AI Engineer

---

### Overview

Extracting data is only half the job. The real value comes from turning that data into reports that tell a story — reports that help you make decisions, spot trends, and stay on budget. In this lesson, you will learn how to use Claude Cowork to generate professional financial reports from your extracted data.

---

### Types of Reports Cowork Can Generate

Claude Cowork can produce a wide range of financial reports. Here are the most common ones:

| Report Type | What It Shows | Best For |
|-------------|--------------|----------|
| **Expense Summary** | Total spending broken down by category | Quick snapshot of where money is going |
| **Monthly Expense Report** | All expenses for a given month, organized and totaled | Regular bookkeeping and review |
| **Budget vs. Actual** | Planned spending compared to real spending | Staying on track with financial goals |
| **Vendor Summary** | Total spending per vendor over a period | Evaluating vendor relationships and negotiating contracts |
| **Category Trend Report** | How spending in each category changes over time | Identifying patterns and seasonal fluctuations |
| **Quarterly Business Report** | Comprehensive summary of income, expenses, and net position | Board meetings, investor updates, or personal review |

---

### Example: Monthly Expense Report

Let us say you have already processed your receipts and invoices for March 2026 (as covered in the previous lessons). Now you want a clean report.

**Your prompt:**

> Generate a monthly expense report from my processed invoices for March 2026. Group expenses by category, show subtotals for each category, and include a grand total at the bottom. Add a summary section at the top with total spending, number of transactions, and the largest single expense.

**What Cowork delivers:**

A formatted report that might include:

**Summary**
- Total Spending: $4,425.75
- Number of Transactions: 47
- Largest Single Expense: Delta Airlines — $342.00 (Travel)
- Most Active Category: Office Supplies (18 transactions)

**Breakdown by Category**

| Category | Transactions | Total |
|----------|-------------|-------|
| Office Supplies | 18 | $1,523.40 |
| Travel | 5 | $1,287.00 |
| Software | 8 | $892.00 |
| Meals | 12 | $534.85 |
| Miscellaneous | 4 | $188.50 |
| **Grand Total** | **47** | **$4,425.75** |

---

### Creating Charts and Visualizations

Numbers in a table are useful, but a chart can make the story instantly clear. Cowork can generate visual representations of your data.

**Pie chart for category breakdown:**

> Create a pie chart showing what percentage of my March 2026 spending went to each category.

**Bar chart for monthly comparison:**

> Create a bar chart comparing my total spending for January, February, and March 2026.

**Line chart for trends:**

> Create a line chart showing my weekly spending over the past 3 months.

Cowork generates these charts as images that you can embed in presentations, emails, or documents. You can also request them as part of an Excel file, where they appear as native spreadsheet charts.

**Tip:** When requesting charts, mention the specific chart type you want. If you leave it open, Cowork will pick the format it thinks fits best — but your preference always wins.

---

### Comparing Periods

One of the most powerful uses of financial reports is comparison. Seeing how this month stacks up against last month — or this quarter against the same quarter last year — reveals trends you might otherwise miss.

#### Month-over-Month Comparison

**Your prompt:**

> Compare my expenses for February 2026 and March 2026. Show each category side by side with the dollar difference and percentage change. Highlight any category where spending increased by more than 20%.

**Sample output:**

| Category | Feb 2026 | Mar 2026 | Change ($) | Change (%) | Flag |
|----------|----------|----------|-----------|-----------|------|
| Office Supplies | $1,100.00 | $1,523.40 | +$423.40 | +38.5% | Over 20% |
| Travel | $1,450.00 | $1,287.00 | -$163.00 | -11.2% | |
| Software | $892.00 | $892.00 | $0.00 | 0.0% | |
| Meals | $380.00 | $534.85 | +$154.85 | +40.8% | Over 20% |
| Miscellaneous | $210.00 | $188.50 | -$21.50 | -10.2% | |
| **Total** | **$4,032.00** | **$4,425.75** | **+$393.75** | **+9.8%** | |

#### Year-over-Year Comparison

**Your prompt:**

> Compare Q1 2025 and Q1 2026 expenses. Show the total for each quarter, the difference, and a category-by-category breakdown.

This is especially useful for spotting long-term trends — for instance, if software costs have been creeping up year after year.

---

### Exporting and Sharing Reports

Once your report is ready, you need to get it into the right hands. Here are your options:

| Format | How to Request | Best For |
|--------|---------------|----------|
| **Excel (.xlsx)** | "Save the report as an Excel file" | Colleagues who use spreadsheets daily |
| **PDF** | "Export the report as a PDF" | Formal sharing, printing, or archiving |
| **CSV** | "Save it as a CSV" | Importing into accounting software or databases |
| **Google Sheets** | "Create a Google Sheets compatible file" | Teams that collaborate in Google Workspace |

You can also ask Cowork to format the report for a specific audience:

> Format this report for my manager. Keep it to one page with a summary at the top and the detailed breakdown below.

> Make this report presentation-ready with clean formatting and charts I can paste into a slide deck.

---

### Real-World Example: Small Business Quarterly Report

Let us walk through a realistic scenario from start to finish.

#### The Situation

You run a small design studio with 5 employees. It is the end of Q1 2026, and you need to prepare a quarterly financial summary for your business partner.

#### Step 1 — Gather the Data

You have already been processing receipts and invoices throughout the quarter (using the workflows from Lessons 1 and 2). Your processed spreadsheets are saved in your Reports folder, one per month.

#### Step 2 — Generate the Quarterly Report

**Your prompt:**

> I have three monthly expense spreadsheets in my Reports folder: January-2026.xlsx, February-2026.xlsx, and March-2026.xlsx. Combine them into a single Q1 2026 quarterly report. Include the following sections: (1) Executive summary with total revenue, total expenses, and net profit. (2) Monthly breakdown showing spending by category for each month. (3) Top 10 vendors by total spend. (4) Month-over-month trend for each category. (5) A bar chart comparing monthly totals. Format everything cleanly and save as both Excel and PDF.

#### Step 3 — Review the Output

Cowork produces two files:

- `Q1-2026-Quarterly-Report.xlsx` — Full report with all sections, charts, and detailed data in separate sheets.
- `Q1-2026-Quarterly-Report.pdf` — A polished, print-ready version.

#### What the Report Includes

**Executive Summary**
- Total Revenue: $48,500.00
- Total Expenses: $13,285.75
- Net Profit: $35,214.25
- Profit Margin: 72.6%

**Monthly Breakdown**

| Category | January | February | March | Q1 Total |
|----------|---------|----------|-------|----------|
| Office Supplies | $1,050.00 | $1,100.00 | $1,523.40 | $3,673.40 |
| Travel | $890.00 | $1,450.00 | $1,287.00 | $3,627.00 |
| Software | $892.00 | $892.00 | $892.00 | $2,676.00 |
| Meals | $310.00 | $380.00 | $534.85 | $1,224.85 |
| Miscellaneous | $695.50 | $210.00 | $188.50 | $1,094.00 |
| Utilities | $340.00 | $310.50 | $340.00 | $990.50 |
| **Total** | **$4,177.50** | **$4,342.50** | **$4,765.75** | **$13,285.75** |

**Top 5 Vendors**

| Rank | Vendor | Q1 Total |
|------|--------|----------|
| 1 | Delta Airlines | $2,180.00 |
| 2 | Adobe | $1,788.00 |
| 3 | Office Depot | $1,445.00 |
| 4 | WeWork | $1,200.00 |
| 5 | Amazon | $987.50 |

#### Step 4 — Share It

Send the PDF to your business partner and keep the Excel version for your records. If questions come up, the detailed spreadsheet has all the supporting data.

---

### What You Have Learned

In this lesson, you learned how to:

- Generate different types of financial reports from extracted data.
- Create charts and visualizations to make the numbers easier to understand.
- Compare spending across different time periods to spot trends.
- Export reports in the right format for any audience.
- Put it all together for a real-world quarterly business report.

---

### What Is Next

In **Module 05 — Web Research**, you will learn how to use Claude Cowork to gather information from the web, summarize articles, and compile research reports — all without leaving your workspace.

---

### Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 04 — Data Extraction & Reporting](README.md) |
| Previous Lesson | [Lesson 2 — Receipt Processing](receipt-processing.md) |
| Next Module | [Module 05 — Web Research](../05-web-research/) |
| Course Home | [Course Home](../../README.md) |
