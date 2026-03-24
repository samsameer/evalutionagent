# Prompt Templates

**Claude Cowork Mastery — March 2026**
**By Jabbir Basha, Principal AI Engineer**

---

Copy-paste these prompts directly into Claude Cowork. Replace anything in `[brackets]` with your specific details.

---

## File Management Prompts

### Sort Files by Type
```
Look at all the files in my [Downloads] folder. Sort them into subfolders by file type:
- PDFs → Documents/
- Images (jpg, png, gif) → Images/
- Spreadsheets (xlsx, csv) → Spreadsheets/
- Everything else → Other/

Do not delete any files. Just move them into the right subfolder.
```

### Rename Files with Consistent Naming
```
Go through all the PDF files in my [Invoices] folder. Rename each one using this format:
YYYY-MM-DD_[VendorName]_Invoice.pdf

Use the date and vendor name from the content of each PDF. If you can't determine the date or vendor, keep the original filename but add a "NEEDS-REVIEW_" prefix.
```

### Organize Project Folders
```
I have a messy folder at [path/to/folder] with files from multiple projects. Please:
1. Identify which project each file belongs to based on its name and content
2. Create a subfolder for each project
3. Move files into their respective project folders
4. Create a summary file listing what was moved where
```

### Clean Up Duplicate Files
```
Scan my [Documents] folder for duplicate files (same name or same content). Create a report showing:
- File name
- Location of each copy
- File size
- Which copy is newer

Do NOT delete anything yet. Just give me the report so I can decide what to keep.
```

---

## Data Extraction Prompts

### Extract Data from PDFs to Spreadsheet
```
Read all the PDF invoices in my [Invoices/2026] folder. Create an Excel spreadsheet with these columns:
- Invoice Date
- Vendor Name
- Invoice Number
- Amount (before tax)
- Tax Amount
- Total Amount
- Category (try to determine from vendor name or description)

Save the spreadsheet as "Invoice_Summary_[Month]_2026.xlsx" in the same folder.
```

### Process Receipts
```
Go through all the receipt images and PDFs in my [Receipts/March] folder. Extract the following from each:
- Date of purchase
- Store/vendor name
- Total amount
- Payment method (if visible)
- Items purchased (if legible)

Create a spreadsheet called "Receipts_March_2026.xlsx" with all this data. Add a "Category" column and categorize each expense (Office Supplies, Travel, Meals, Software, etc.).
```

### Generate Monthly Expense Report
```
Using the data in my [Expenses/2026] folder, generate a monthly expense report for [March 2026] that includes:
1. Total expenses for the month
2. Breakdown by category (pie chart if possible)
3. Top 5 largest expenses
4. Comparison with [February 2026] if data is available
5. Any unusual or flagged expenses

Save the report as "Expense_Report_March_2026.xlsx" in my [Reports] folder.
```

---

## Web Research Prompts

### Competitor Analysis
```
Research the following competitors in the [industry] space:
[Competitor 1, Competitor 2, Competitor 3]

For each competitor, find:
- Their main product/service offerings
- Pricing (if publicly available)
- Key features or differentiators
- Recent news or updates (last 3 months)
- Customer review sentiment (positive/negative themes)

Create a comparison spreadsheet and save it to my [Research] folder as "Competitor_Analysis_March_2026.xlsx"
```

### Market Research
```
Research the current state of the [industry/market] in [region/country]. I need:
1. Market size and growth trends
2. Top 5 players and their market share
3. Emerging trends and opportunities
4. Potential risks or challenges
5. Key statistics and data points

Compile everything into a 2-page executive summary. Save it as "Market_Research_[Industry]_March_2026.md" in my [Research] folder.
```

### Property/Real Estate Research
```
Search for new [commercial/residential] property listings in [location/area] that meet these criteria:
- Price range: [min] to [max]
- Size: at least [X] sq ft
- Type: [apartment/house/office/retail]

Create a spreadsheet with:
- Property address
- Listing price
- Size (sq ft)
- Price per sq ft
- Key features
- Listing URL
- Date listed

Save as "Property_Listings_[Location]_[Date].xlsx" in my [Research/Properties] folder.
```

---

## Automation & Scheduling Prompts

### Weekly File Cleanup
```
Every [Monday] at the start of the week, please:
1. Check my [Downloads] folder for any new files
2. Sort them into the appropriate subfolders (Documents, Images, Spreadsheets, Other)
3. Rename any files that don't follow the naming convention
4. Create a log file called "Cleanup_Log_[Date].txt" summarizing what was done
```

### Daily Research Monitor
```
Every [weekday morning], please:
1. Search for new [property listings / industry news / competitor updates]
2. Compare with yesterday's results to identify what's new
3. Add new entries to the master tracking spreadsheet at [path]
4. If anything matches my criteria [describe criteria], highlight it in the spreadsheet
5. Save a brief summary in my [Reports/Daily] folder
```

### Monthly Reporting Automation
```
On the [1st of every month], please:
1. Gather all invoice and receipt data from the previous month's folder
2. Generate a monthly expense summary spreadsheet
3. Create a comparison with the previous month
4. Flag any expenses over [amount]
5. Save the report in [Reports/Monthly/] with the naming format "Monthly_Report_YYYY_MM.xlsx"
```

---

## Tips for Better Prompts

1. **Be specific** — Include exact folder paths, file names, and formats
2. **Give examples** — Show the naming convention or format you want
3. **Set boundaries** — Say what NOT to do (e.g., "Do not delete any files")
4. **Request confirmation** — Add "Ask me before making any changes" for sensitive tasks
5. **Iterate** — Start simple, then add complexity as you see results

---

[← Back to Templates](README.md) | [Back to Course Home](../README.md)
