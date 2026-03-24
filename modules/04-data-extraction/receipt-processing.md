# Module 04, Lesson 2 | Claude Cowork Mastery — March 2026

## Receipt and Invoice Processing

**Instructor:** Jabbir Basha, Principal AI Engineer

---

### Common Receipt and Invoice Processing Challenges

If you have ever tried to organize a shoebox full of receipts at tax time, you know the pain. Here are the challenges most people and businesses face:

- **Volume** — A small business can generate hundreds of receipts per month. Manually entering each one is not sustainable.
- **Inconsistent formats** — Every vendor uses a different layout, font size, and field arrangement.
- **Faded or damaged prints** — Thermal paper receipts fade over time, making them hard to read.
- **Missing information** — Some receipts lack key details like a clear date or itemized breakdown.
- **Currency and tax variation** — International purchases or multi-state operations add layers of complexity.

Claude Cowork is built to handle all of these. You give it the receipts, tell it what you need, and it does the heavy lifting.

---

### Setting Up Your Receipt Scanning Workflow

A reliable workflow starts with good habits. Here is a simple system you can put in place today.

#### Step 1 — Create a Folder Structure

Set up folders like this:

```
Receipts/
    Inbox/          (drop new receipts here)
    Processed/      (Cowork moves files here after extraction)
    Reports/        (final spreadsheets and summaries go here)
```

#### Step 2 — Capture Your Receipts

You have several options:

- **Phone camera** — Take a photo of each paper receipt and save it to the Inbox folder.
- **Scanner** — Use a flatbed or document scanner for higher quality.
- **Email forwarding** — Many vendors send digital receipts by email. Save those PDFs directly to Inbox.
- **Screenshots** — For online purchases, a screenshot of the confirmation page works too.

#### Step 3 — Run Cowork on the Inbox

Once you have a batch ready, use a prompt like:

> Process all the receipts in my Receipts/Inbox folder. Extract the date, vendor name, total amount, tax amount, and category. Save the results as a spreadsheet in my Receipts/Reports folder.

#### Step 4 — Review and Archive

Check the output spreadsheet, make any corrections, and move the original files from Inbox to Processed so you do not reprocess them.

---

### Example: Processing a Month of Receipts

Let us say it is the end of March and you have 47 receipts sitting in your Inbox folder — a mix of photos, scanned PDFs, and digital receipts from email.

**Your prompt:**

> I have 47 receipts in my Receipts/Inbox folder. Go through each one and create a spreadsheet with the following columns: date, vendor, description, category, subtotal, tax, and total. Categorize each receipt as one of the following: Office Supplies, Travel, Meals, Software, or Miscellaneous. Sort by date and include a total row at the bottom.

**What Cowork delivers:**

A spreadsheet with 47 rows (plus the total row), each receipt neatly categorized and totaled. The output might look like this:

| Date | Vendor | Description | Category | Subtotal | Tax | Total |
|------|--------|-------------|----------|----------|-----|-------|
| 2026-03-01 | Delta Airlines | Flight to Chicago | Travel | $342.00 | $0.00 | $342.00 |
| 2026-03-02 | Office Depot | Printer paper, toner | Office Supplies | $89.50 | $7.16 | $96.66 |
| 2026-03-03 | Chipotle | Team lunch | Meals | $45.80 | $3.66 | $49.46 |
| ... | ... | ... | ... | ... | ... | ... |
| **Total** | | | | **$4,127.30** | **$298.45** | **$4,425.75** |

---

### Extracting Key Fields

Here are the fields Cowork can reliably extract from most receipts and invoices:

| Field | Description | Notes |
|-------|-------------|-------|
| **Date** | Transaction or invoice date | Cowork normalizes dates to a consistent format (e.g., YYYY-MM-DD). |
| **Vendor** | Business or store name | Pulled from the header or logo area of the receipt. |
| **Amount** | Total charge | The bottom-line number you paid. |
| **Tax** | Tax amount | Separated out when listed on the receipt. |
| **Category** | Expense type | You can provide your own category list or let Cowork suggest categories. |
| **Invoice/Receipt Number** | Reference ID | Useful for matching with bank statements. |
| **Payment Method** | Card type or cash | When visible on the receipt. |
| **Line Items** | Individual products or services | Available when the receipt includes an itemized breakdown. |

If a field is not visible on a particular receipt, Cowork will leave that cell blank rather than guess.

---

### Handling Multiple Currencies and Formats

Working with international vendors or traveling abroad means dealing with different currencies. Here is how to handle it.

**Option 1 — Keep original currencies:**

> Extract all receipt data and keep the amounts in their original currency. Add a "Currency" column.

This gives you a raw record of what was charged in each currency.

**Option 2 — Convert to a single currency:**

> Extract all receipt data and convert every amount to USD. Use today's exchange rate. Add columns for original currency, original amount, and converted amount.

Cowork will convert the amounts and show its work so you can verify.

**Handling different date formats:**

Receipts from different countries may show dates as DD/MM/YYYY, MM/DD/YYYY, or other variations. Cowork recognizes these automatically and can normalize everything to a single format of your choice.

**Handling different languages:**

Receipts in other languages are not a problem. Cowork can read receipts in most major languages and extract the data into English (or any other language you prefer).

---

### Tips for Best Results

#### Photo Quality Matters

- **Lay the receipt flat** on a contrasting surface (white receipt on a dark table, or vice versa).
- **Use good lighting** — natural light or a bright lamp. Avoid shadows across the text.
- **Fill the frame** — get close enough that the text is legible, but capture the entire receipt.
- **Avoid blur** — hold steady or prop your phone against something stable.

#### Folder Organization

- **Process regularly** — weekly or biweekly batches are easier to manage than a quarterly dump.
- **Name files descriptively** when you can (e.g., `2026-03-15-Staples.jpg` is better than `IMG_4872.jpg`).
- **Separate by month or project** if you deal with high volumes.

#### Prompt Clarity

- **Specify your categories** up front so Cowork uses your system rather than inventing its own.
- **State the output format** you want (CSV, Excel, etc.).
- **Mention any special rules** — for example, "Flag any receipt over $500" or "Exclude personal purchases."

---

### Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 04 — Data Extraction & Reporting](README.md) |
| Previous Lesson | [Lesson 1 — PDF to Spreadsheet](pdf-to-spreadsheet.md) |
| Next Lesson | [Lesson 3 — Financial Reports](financial-reports.md) |
| Course Home | [Course Home](../../README.md) |
