# Module 06, Lesson 2 | Claude Cowork Mastery — March 2026

**Instructor:** Jabbir Basha, Principal AI Engineer

---

# Building Automation Workflows

In this lesson, you will learn how to chain multiple tasks together into multi-step workflows. Instead of automating one task at a time, you can create sequences where the output of one step feeds directly into the next.

---

## What Is a Multi-Step Workflow?

A multi-step workflow is a series of tasks that run in a defined order, where each step builds on the results of the previous one. Think of it like an assembly line — each station performs a specific job and passes the result along to the next station.

**Single task:** "Summarize this report."

**Multi-step workflow:** "Download the latest sales report, extract the key metrics, compare them to last month, and create a summary with highlights and concerns."

The power of workflows is that Cowork handles every step automatically, from start to finish.

---

## Chaining Tasks Together

To build a workflow, you describe the sequence of steps in your instruction. Cowork will execute them in order, passing results from one step to the next.

**General pattern:**

> "First, do [Step 1]. Then, take the result and [Step 2]. Next, [Step 3]. Finally, [Step 4]."

**Example:**

> "Download the latest inventory spreadsheet from the shared folder. Extract all items where stock is below 50 units. Create a reorder list with item names, current stock levels, and suggested reorder quantities. Save the reorder list to the Purchasing folder."

**The workflow chain:**

1. **Download** — Retrieve the source file
2. **Extract** — Pull out the relevant data
3. **Process** — Transform the data into something useful
4. **Report** — Save the final output

---

## Conditional Logic in Workflows

You can add decision points to your workflows using simple "if/then" language. This lets Cowork take different actions depending on what it finds.

**Example:**

> "If the expense total exceeds $5,000, flag it for review and save it to the Flagged Expenses folder. Otherwise, file it in the Approved Expenses folder."

**More examples of conditional logic:**

- "If the report contains any negative growth figures, highlight them in red and add a note at the top."
- "If there are more than 20 new listings, only include the top 10 by price in the summary."
- "If the file is older than 30 days, archive it instead of processing it."

Conditional logic makes your workflows smarter and more adaptable to different situations.

---

## Example Workflow: Daily Property Listing Monitor

Here is a complete multi-step workflow for monitoring real estate listings. This example shows how several tasks can be chained together into a single automation.

**Instruction:**

> "Every morning at 8 AM, run the following workflow:
>
> 1. Search real estate listing sites for new properties posted in the last 24 hours in the Austin, TX metro area.
> 2. For each new listing, extract the price, location, square footage, number of bedrooms, and listing date.
> 3. Add each listing as a new row in the master property spreadsheet in my Real Estate folder.
> 4. Flag any listings that match my criteria: under $400,000, at least 3 bedrooms, and within 15 miles of downtown.
> 5. Create a daily summary of flagged listings and save it to my Real Estate Reports folder."

**How the workflow executes:**

| Step | Action | Output |
|------|--------|--------|
| 1 | Search for new listings | Raw listing data |
| 2 | Extract key details | Structured property information |
| 3 | Update master spreadsheet | Spreadsheet with new rows added |
| 4 | Apply matching criteria | Flagged listings identified |
| 5 | Generate summary report | Daily report saved to folder |

Each step depends on the one before it, and Cowork handles the entire sequence without any intervention from you.

---

## Creating Workflow Templates for Reuse

If you find yourself building similar workflows for different purposes, you can create reusable templates. A template is simply a well-structured workflow instruction that you can adapt by changing a few details.

**Template example — Data Collection Workflow:**

> "Every [frequency], do the following:
> 1. Search [source] for new [items] from the last [time period].
> 2. Extract [specific fields] from each item.
> 3. Add the data to [destination spreadsheet].
> 4. Flag items matching [criteria].
> 5. Save a summary report to [output folder]."

**Using the template:**

To create a new workflow, simply fill in the bracketed sections with your specific details. This approach saves time and ensures consistency across your automations.

**Tips for effective templates:**
- Keep the structure general enough to apply to multiple use cases
- Use clear placeholder labels so you remember what to fill in
- Save your templates in a dedicated folder for easy reference

---

## Error Handling in Automations

Even well-designed workflows can encounter problems. Here is how to build resilience into your automations:

### Common Issues and How to Address Them

| Issue | Solution |
|-------|----------|
| Source file is missing or unavailable | Add an instruction: "If the file is not found, skip this step and note it in the log." |
| Data format has changed | Include a fallback: "If the expected columns are not present, save the raw data and flag for manual review." |
| Too much data to process at once | Set limits: "Process only the first 100 items. If there are more, note the total count in the report." |
| Output folder does not exist | Specify: "If the output folder does not exist, create it." |

### General Error Handling Tips

1. **Anticipate what can go wrong** — Think about each step and what might fail
2. **Include fallback instructions** — Tell Cowork what to do when something unexpected happens
3. **Request logging** — Ask Cowork to note any issues it encounters during the workflow
4. **Start with small runs** — Test your workflow on a small dataset before running it at full scale
5. **Review the first few runs** — Check the output carefully during the initial runs to catch any issues early

---

## Summary

Multi-step workflows let you automate complex processes by chaining tasks together in a defined sequence. By adding conditional logic, creating reusable templates, and building in error handling, you can create powerful automations that handle sophisticated work reliably and consistently.

---

## Navigation

| Direction | Link |
|-----------|------|
| Previous Lesson | [Creating Recurring Tasks](recurring-tasks.md) |
| Module Home | [Module 06: Scheduled Automations](README.md) |
| Next Lesson | [Monitoring Automation Results](monitoring-results.md) |
| Course Home | [Back to Course Home](../../README.md) |
