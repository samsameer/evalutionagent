# Module 08, Lesson 1 | Claude Cowork Mastery — March 2026

**Instructor:** Jabbir Basha, Principal AI Engineer

---

# Property Management Automation

## Project Overview

In this project, you will build a **complete property management automation system** using Claude Cowork. Property and real estate administration involves a large volume of repetitive tasks — organizing lease documents, tracking rent payments, monitoring local market conditions, and generating performance reports. By the end of this lesson, you will have a working system that handles all of these tasks with minimal manual effort.

**Who is this for?** Property managers, landlords, real estate investors, or anyone responsible for managing rental properties and their associated paperwork.

**What you will build:**
- An organized folder structure for all property-related documents
- A rent tracking spreadsheet populated from lease agreements
- Automated market research for local property listings
- Monthly property performance reports
- A recurring automation that keeps everything up to date

---

## Step 1: Set Up Your Property Folder Structure

The foundation of any good management system is organization. Start by creating a clear folder structure that separates properties, tenants, and document types.

### Prompt Template

```
Create the following folder structure for my property management system:

property-management/
  properties/
    unit-101/
      lease-agreements/
      maintenance-records/
      photos/
    unit-102/
      lease-agreements/
      maintenance-records/
      photos/
    unit-103/
      lease-agreements/
      maintenance-records/
      photos/
  tenants/
    current/
    past/
  financial/
    rent-tracking/
    expenses/
    tax-documents/
  reports/
    monthly/
    quarterly/
  market-research/

Also create a README file inside the property-management folder that explains what each folder is for.
```

### What to Expect

Claude Cowork will create the entire folder tree and generate a README file that serves as a quick reference for anyone accessing the system. You should see all folders created with confirmation messages.

---

## Step 2: Organize Lease Agreements and Property Documents

Now that you have a structure in place, use Cowork to organize your existing documents into the correct locations and extract key details from them.

### Prompt Template

```
I have the following lease agreement details. Please create a lease summary document for each unit and save it in the appropriate folder:

Unit 101:
- Tenant: Sarah Johnson
- Lease start: January 1, 2026
- Lease end: December 31, 2026
- Monthly rent: $1,450
- Security deposit: $1,450
- Pet deposit: $300

Unit 102:
- Tenant: Marcus Williams
- Lease start: March 1, 2026
- Lease end: February 28, 2027
- Monthly rent: $1,600
- Security deposit: $1,600
- Pet deposit: None

Unit 103:
- Tenant: Priya Patel
- Lease start: February 15, 2026
- Lease end: February 14, 2027
- Monthly rent: $1,350
- Security deposit: $1,350
- Pet deposit: $250

For each unit, create a structured summary document that includes all key dates, amounts, and tenant contact placeholders. Save each file as lease-summary.md in the corresponding unit's lease-agreements folder.
```

### What to Expect

You will get three neatly formatted lease summary documents, each saved in the correct unit folder. These serve as quick-reference documents so you never have to dig through full lease contracts for basic information.

---

## Step 3: Extract Rent Data into a Tracking Spreadsheet

With lease details organized, the next step is to create a centralized rent tracking system.

### Prompt Template

```
Using the lease summaries in my property-management/properties/ folders, create a rent tracking spreadsheet as a CSV file saved to property-management/financial/rent-tracking/rent-tracker-2026.csv.

The spreadsheet should include:
- Columns: Unit, Tenant Name, Monthly Rent, Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, Dec, Total Collected, Balance Due
- One row per unit (101, 102, 103)
- Mark January through March as "Paid" for Unit 101
- Mark March as "Paid" for Unit 102
- Mark February and March as "Paid" for Unit 103
- All other months should show "Pending"
- Calculate Total Collected and Balance Due based on the paid months

Also create a summary row at the bottom showing totals across all units.
```

### What to Expect

A CSV file that you can open in any spreadsheet application. The tracker gives you a single view of all rent collection across your properties, making it easy to see who has paid and what is outstanding.

---

## Step 4: Monitor Local Property Market Listings

Stay informed about your local market by using Cowork's web research capabilities to gather current listing data.

### Prompt Template

```
Research the current rental market for 2-bedroom apartments in Austin, Texas. I need:

1. Average asking rent for 2-bedroom apartments in the Austin metro area
2. How current rents compare to 6 months ago (up, down, or stable)
3. Vacancy rate trends if available
4. Any notable market developments (new construction, policy changes, etc.)

Save the findings as a market report in property-management/market-research/austin-rental-market-march-2026.md with the following sections:
- Market Summary
- Key Statistics
- Trends and Outlook
- Sources

Keep the language simple and focus on actionable insights for a small-scale landlord.
```

### What to Expect

A concise market report with current data and trends. This helps you make informed decisions about rent pricing, lease renewals, and property investments without spending hours browsing real estate websites.

---

## Step 5: Generate Monthly Property Performance Reports

Combine all your data into a professional monthly report.

### Prompt Template

```
Generate a monthly property performance report for March 2026 using the data in my property-management folder. The report should be saved to property-management/reports/monthly/march-2026-report.md and include:

1. Executive Summary — A 3-4 sentence overview of how the properties performed this month

2. Rent Collection Summary:
   - Total rent expected this month
   - Total rent collected
   - Collection rate (percentage)
   - Any outstanding balances

3. Property Status:
   - Occupancy rate (occupied units vs. total units)
   - Any upcoming lease expirations in the next 90 days
   - Maintenance issues (placeholder section)

4. Market Context:
   - Brief summary from the latest market research report
   - How our rents compare to market averages

5. Action Items:
   - List any follow-up tasks (e.g., "Follow up on Unit 102 March rent" or "Begin lease renewal discussion with Priya Patel")

Format it professionally so it could be shared with a business partner or investor.
```

### What to Expect

A polished, professional report that pulls together rent data, occupancy information, and market context. This is the kind of document that would normally take an hour or more to compile manually.

---

## Step 6: Automate Recurring Rent Tracking and Report Generation

Set up prompts and workflows that you can reuse each month with minimal changes.

### Prompt Template

```
Create a reusable automation checklist saved to property-management/monthly-automation-checklist.md that I can follow at the start of each month. The checklist should include:

1. Update rent tracker:
   - Prompt template to mark payments as received for the previous month
   - Prompt template to flag any late or missing payments

2. Generate market research:
   - Prompt template to pull fresh rental market data for Austin, TX
   - Instructions for updating the market-research folder

3. Generate monthly report:
   - Prompt template for the performance report (with placeholders for the current month)
   - Reminder to review and customize the action items section

4. Tenant communication:
   - Prompt template for a friendly rent reminder email
   - Prompt template for a lease renewal inquiry email

Each prompt template should be copy-paste ready — I just need to update the month and any specific details.
```

### What to Expect

A complete automation playbook that turns your monthly property management tasks into a streamlined, repeatable process. Instead of starting from scratch each month, you simply follow the checklist and paste the prompts.

---

## Expected Outcomes and Deliverables

By the end of this project, you will have created:

| Deliverable | Location |
|-------------|----------|
| Organized folder structure | `property-management/` |
| Lease summary documents | `properties/unit-*/lease-agreements/` |
| Rent tracking spreadsheet | `financial/rent-tracking/rent-tracker-2026.csv` |
| Market research report | `market-research/austin-rental-market-march-2026.md` |
| Monthly performance report | `reports/monthly/march-2026-report.md` |
| Reusable automation checklist | `monthly-automation-checklist.md` |

**Estimated time to complete this project:** 45–60 minutes

**Estimated time saved per month after setup:** 4–6 hours

---

## Key Takeaways

- A well-organized folder structure is the foundation for any automation
- Claude Cowork can extract structured data from documents and compile it into spreadsheets
- Web research keeps you informed about market conditions without manual browsing
- Monthly reports become effortless when you combine organized data with reusable prompts
- Automation checklists turn one-time setups into repeatable workflows

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Overview | [Module 08 README](README.md) |
| Next Lesson | [Lesson 2 — Freelancer Workflow Automation](freelancer-workflow.md) |

---

*Claude Cowork Mastery Tutorial — Module 08, Lesson 1 of 3*
*Author: Jabbir Basha, Principal AI Engineer — March 2026*
