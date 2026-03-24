# Module 06, Lesson 3 | Claude Cowork Mastery — March 2026

**Instructor:** Jabbir Basha, Principal AI Engineer

---

# Monitoring and Reviewing Automation Results

In this lesson, you will learn how to monitor the output of your automations, review results for quality, handle errors, and refine your workflows over time. Setting up an automation is only half the job — keeping it running well requires ongoing attention.

---

## Where Cowork Stores Automation Output

When your automations run, Cowork saves the results to the locations you specify in your instructions. If you do not specify a location, Cowork will use a default output area.

**Best practice:** Always include an explicit output location in your instructions so you always know where to find results.

**Example:**

> "Save the weekly summary report to my Automation Reports folder, using the format Weekly-Summary-YYYY-MM-DD."

This ensures every output is easy to find and clearly dated.

---

## Setting Up an Output and Reports Folder

A well-organized folder structure makes monitoring much easier. Here is a recommended setup:

```
Automations/
    Reports/
        Daily/
        Weekly/
        Monthly/
    Logs/
    Archive/
```

| Folder | Purpose |
|--------|---------|
| **Reports/Daily** | Stores output from daily automations |
| **Reports/Weekly** | Stores output from weekly automations |
| **Reports/Monthly** | Stores output from monthly automations |
| **Logs** | Stores run logs and error reports |
| **Archive** | Stores older reports you want to keep but do not need readily accessible |

Setting up this structure before you start building automations will keep everything organized from the beginning.

---

## Reviewing Automation Logs

Automation logs tell you what happened during each run. They are your primary tool for understanding whether an automation completed successfully or encountered issues.

**What to look for in logs:**

- **Completion status** — Did the automation finish all steps?
- **Items processed** — How many items were handled? Does this match expectations?
- **Warnings or notes** — Did Cowork flag anything unusual?
- **Errors** — Were there any failures during the run?
- **Timing** — How long did the automation take? Is it slowing down over time?

**Tip:** Ask Cowork to include a brief status summary at the top of each log file so you can quickly assess the run without reading the full log.

> "At the top of each log file, include a summary line with: date, number of items processed, number of errors, and overall status (success or needs attention)."

---

## Quality Checking Automated Outputs

Automation saves time, but it is important to verify that the outputs are accurate and useful. Here is a practical approach to quality checking:

### Spot-Check Method

1. **Pick a few items at random** from the output
2. **Verify them manually** against the source data
3. **Compare the format** to your expectations — is the layout correct? Are all fields present?
4. **Check the edges** — look at the first and last items to make sure nothing was cut off

### Quality Checklist

- Are all expected fields present in the output?
- Do the numbers add up correctly?
- Is the formatting consistent across all entries?
- Are dates and names accurate?
- Does the output match what you would have produced manually?

### How Often to Quality Check

| Automation Age | Recommended Frequency |
|---------------|----------------------|
| First 2 weeks | Check every run |
| Weeks 3 through 4 | Check every other run |
| After 1 month | Spot-check weekly |
| After 3 months | Spot-check monthly (if consistently accurate) |

As you gain confidence in an automation, you can reduce the frequency of your checks.

---

## Handling Errors and Failed Tasks

When an automation encounters an error, here is how to respond:

### Step-by-Step Error Resolution

1. **Read the error log** — Understand what went wrong and at which step
2. **Identify the cause** — Common causes include missing files, changed data formats, or access issues
3. **Fix the underlying issue** — Address the root cause, not just the symptom
4. **Re-run the automation manually** — Test the fix before letting it run on schedule again
5. **Update the instruction if needed** — Add error handling to prevent the same issue in the future

### Common Errors and Fixes

| Error | Likely Cause | Fix |
|-------|-------------|-----|
| "File not found" | Source file was moved or renamed | Update the file path in your instruction |
| Incomplete output | Data format changed | Review the source and adjust extraction instructions |
| Duplicate entries | Automation ran twice | Check the schedule and add deduplication logic |
| Empty report | No new data to process | Add a note: "If no new items are found, log that and skip the report" |

---

## Adjusting Automations Based on Results

Your automations will likely need fine-tuning over time. Here are common adjustments:

- **Refine the instructions** — If the output is not quite right, make the instructions more specific
- **Change the frequency** — If a daily task only produces meaningful results once a week, switch to weekly
- **Add or remove steps** — As your needs change, update the workflow to match
- **Update criteria** — Adjust thresholds, filters, or matching criteria based on what you are seeing in the results
- **Expand scope** — Once an automation is running well, consider adding more sources or data points

**Tip:** Keep a simple changelog for each automation. Note what you changed and when, so you can trace issues back to specific adjustments.

---

## Example: Weekly Review of Automated Research Reports

Here is a practical example of how to monitor a recurring automation that generates research reports.

**The automation:**

> "Every Wednesday, search for new articles on renewable energy policy, summarize the top five, and save the report to my Research Reports folder."

**Weekly review process:**

1. **Open the latest report** from the Research Reports folder
2. **Check the article count** — Are there five summaries as expected?
3. **Scan the sources** — Are the articles from reputable publications?
4. **Read one or two summaries** — Do they accurately reflect the original articles?
5. **Check for relevance** — Are all articles actually about renewable energy policy, or has the scope drifted?
6. **Note any issues** — If something needs improvement, update the instruction before the next run

**Example feedback to Cowork:**

> "The last report included an article about electric vehicle sales, which is not directly about energy policy. Please focus strictly on policy and regulation topics, not industry or market news."

This kind of iterative refinement improves the automation over time.

---

## Tips for Maintaining Automation Quality Over Time

1. **Schedule a monthly automation review** — Set aside 15 to 30 minutes once a month to review all active automations
2. **Archive old reports** — Move outdated output to an archive folder to keep your workspace clean
3. **Retire automations you no longer need** — If a task is no longer relevant, pause or delete the automation
4. **Document your automations** — Keep a simple list of what each automation does, when it runs, and where it saves output
5. **Start small and grow** — It is better to have a few reliable automations than many unreliable ones
6. **Share what works** — If you find an automation that saves significant time, consider sharing the approach with colleagues

---

## Summary

Monitoring your automations is essential for maintaining quality and reliability. By organizing your output folders, reviewing logs, spot-checking results, and making adjustments based on what you find, you ensure that your automations continue to deliver value over time. The goal is to reach a point where your automations run reliably with only occasional oversight.

---

## Navigation

| Direction | Link |
|-----------|------|
| Previous Lesson | [Building Automation Workflows](automation-workflows.md) |
| Module Home | [Module 06: Scheduled Automations](README.md) |
| Course Home | [Back to Course Home](../../README.md) |
