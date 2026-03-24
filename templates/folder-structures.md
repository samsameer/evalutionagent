# Recommended Folder Structures

**Claude Cowork Mastery — March 2026**
**By Jabbir Basha, Principal AI Engineer**

---

Set up these folder structures before giving Claude Cowork access. A clean starting structure helps Cowork organize your files effectively and consistently.

---

## General Business Folder Structure

```
Business/
├── Clients/
│   ├── Client-A/
│   │   ├── Contracts/
│   │   ├── Invoices/
│   │   ├── Deliverables/
│   │   └── Communications/
│   └── Client-B/
│       ├── Contracts/
│       ├── Invoices/
│       ├── Deliverables/
│       └── Communications/
│
├── Finance/
│   ├── Income/
│   │   ├── 2026-01/
│   │   ├── 2026-02/
│   │   └── 2026-03/
│   ├── Expenses/
│   │   ├── 2026-01/
│   │   ├── 2026-02/
│   │   └── 2026-03/
│   ├── Receipts/
│   ├── Tax/
│   └── Reports/
│       ├── Monthly/
│       ├── Quarterly/
│       └── Annual/
│
├── Research/
│   ├── Market-Analysis/
│   ├── Competitors/
│   ├── Properties/
│   └── Reports/
│
├── Operations/
│   ├── Templates/
│   ├── Processes/
│   └── Checklists/
│
└── Cowork-Output/
    ├── Daily/
    ├── Weekly/
    ├── Reports/
    └── Logs/
```

---

## Freelancer Folder Structure

```
Freelance/
├── Active-Projects/
│   ├── ProjectName-ClientName/
│   │   ├── Brief/
│   │   ├── Work-in-Progress/
│   │   ├── Deliverables/
│   │   ├── Feedback/
│   │   └── Invoice/
│   └── ...
│
├── Completed-Projects/
│   └── YYYY-MM-ProjectName/
│
├── Proposals/
│   ├── Sent/
│   └── Templates/
│
├── Finance/
│   ├── Invoices-Sent/
│   ├── Invoices-Paid/
│   ├── Expenses/
│   ├── Receipts/
│   └── Tax-Documents/
│
├── Portfolio/
│   ├── Case-Studies/
│   └── Samples/
│
├── Research/
│   ├── Market-Rates/
│   ├── Potential-Clients/
│   └── Industry-Trends/
│
└── Cowork-Output/
    ├── Reports/
    └── Logs/
```

---

## Property Management Folder Structure

```
Properties/
├── Portfolio/
│   ├── Property-Address-1/
│   │   ├── Lease-Agreements/
│   │   ├── Maintenance/
│   │   ├── Inspections/
│   │   ├── Photos/
│   │   └── Financials/
│   └── Property-Address-2/
│       └── ...
│
├── Tenants/
│   ├── Active/
│   │   ├── Tenant-Name/
│   │   │   ├── Application/
│   │   │   ├── Lease/
│   │   │   ├── Payments/
│   │   │   └── Communications/
│   │   └── ...
│   └── Past/
│
├── Finance/
│   ├── Rent-Collected/
│   ├── Expenses/
│   ├── Mortgage/
│   ├── Insurance/
│   └── Reports/
│
├── Market-Research/
│   ├── New-Listings/
│   ├── Comparable-Sales/
│   ├── Market-Reports/
│   └── Opportunities/
│
├── Maintenance/
│   ├── Scheduled/
│   ├── Completed/
│   ├── Vendors/
│   └── Receipts/
│
└── Cowork-Output/
    ├── Daily-Listings/
    ├── Monthly-Reports/
    └── Logs/
```

---

## Small Business Folder Structure

```
MyBusiness/
├── Administration/
│   ├── Legal/
│   ├── Insurance/
│   ├── Licenses/
│   └── Policies/
│
├── Sales/
│   ├── Leads/
│   ├── Proposals/
│   ├── Contracts/
│   └── Reports/
│
├── Finance/
│   ├── Accounts-Receivable/
│   ├── Accounts-Payable/
│   ├── Payroll/
│   ├── Receipts/
│   ├── Bank-Statements/
│   └── Reports/
│
├── Marketing/
│   ├── Campaigns/
│   ├── Content/
│   ├── Analytics/
│   └── Competitor-Research/
│
├── Products-Services/
│   ├── Catalog/
│   ├── Pricing/
│   ├── Inventory/
│   └── Suppliers/
│
├── HR/
│   ├── Employees/
│   ├── Hiring/
│   ├── Training/
│   └── Policies/
│
└── Cowork-Output/
    ├── Daily/
    ├── Weekly/
    ├── Monthly/
    └── Logs/
```

---

## Setup Tips

1. **Create the `Cowork-Output` folder** — This is where Claude saves all generated reports and logs
2. **Use date-based subfolders** for financial data (YYYY-MM format)
3. **Grant Cowork access to the top-level folder** — It can navigate subfolders automatically
4. **Don't share sensitive folders** like passwords, personal medical records, or credentials
5. **Start small** — Begin with one section (like Finance) and expand as you get comfortable

---

## Quick Setup Prompt

Copy this into Cowork to have it create any of these structures:

```
Please create the following folder structure in my [Desktop/Business] folder:
[Paste the structure from above]

Create all folders but don't add any files yet. Confirm when the structure is ready.
```

---

[← Back to Templates](README.md) | [Back to Course Home](../README.md)
