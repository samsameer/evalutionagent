# Assigning Issues to Copilot

**Module 08, Lesson 2 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

There are several ways to trigger the Copilot Coding Agent. This lesson covers all methods and best practices for writing issues that the agent can successfully resolve.

---

## Method 1: Assign the Issue to Copilot

1. Open a GitHub Issue
2. Click the **"Assignees"** section in the sidebar
3. Select **"Copilot"** from the list
4. Copilot begins working on the issue within minutes

---

## Method 2: @copilot Mention in Issue Comments

In any issue comment, type:

```
@copilot Please implement this feature
```

or

```
@copilot Can you fix this bug? The error occurs when the user submits an empty form.
```

Copilot reads the issue context and your comment, then starts working.

---

## Method 3: From Copilot Chat

In the VS Code Copilot Chat panel:

```
@github Create a branch and implement a fix for issue #123
```

---

## Writing Effective Issues for the Coding Agent

The quality of the coding agent's output depends heavily on how well the issue is written.

### Good Issue Template

```markdown
## Description
Add input validation to the user registration form. Currently,
the form accepts any input without checking for valid email
format, password strength, or required fields.

## Requirements
- Email must be a valid email format
- Password must be at least 8 characters with one uppercase,
  one lowercase, and one number
- Username must be 3-30 characters, alphanumeric only
- All fields are required
- Display inline error messages below each field

## Files to Modify
- `src/components/RegisterForm.tsx`
- `src/utils/validation.ts` (create if needed)
- `src/__tests__/RegisterForm.test.tsx` (add validation tests)

## Acceptance Criteria
- [ ] Invalid email shows "Please enter a valid email address"
- [ ] Weak password shows strength requirements
- [ ] Empty fields show "This field is required"
- [ ] Form cannot be submitted with invalid fields
- [ ] All existing tests still pass
- [ ] New tests cover all validation rules
```

### Tips for Better Issues

| Tip | Why |
|-----|-----|
| Be specific about what to change | Agent can plan more accurately |
| List files to modify | Reduces guesswork |
| Include acceptance criteria | Agent knows when it is done |
| Add example code or patterns | Agent follows your style |
| Reference related files | Agent uses them as context |
| Mention the tech stack | Agent uses the right tools |

### What to Avoid

- Vague descriptions: "Make it better" or "Fix the UI"
- Multiple unrelated tasks in one issue
- Issues that require external service access (unless configured)
- Issues that depend on unreleased features or PRs

---

## Monitoring Progress

After assigning an issue to Copilot:

1. **GitHub notifications** — You will receive updates as Copilot works
2. **Issue comments** — Copilot may post status updates on the issue
3. **PR notification** — You will be notified when the PR is created
4. **Session log** — The PR includes a log of Copilot's reasoning process

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 08: Coding Agent](README.md) |
| Previous Lesson | [What is the Coding Agent?](what-is-coding-agent.md) |
| Next Lesson | [Reviewing Agent Pull Requests](reviewing-agent-prs.md) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
