# Prompt Engineering for Claude Code

**Module 11, Lesson 3 — Claude Code Mastery**

**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Overview

Claude Code is only as effective as the instructions you give it. This lesson teaches you how to write prompts that produce accurate, first-try results. You will learn patterns for common tasks, anti-patterns to avoid, and when to let Claude figure things out versus when to be explicit.

---

## 1. Be Specific, Not Vague

The single biggest improvement you can make is being specific about what you want.

### Bad (Vague)

```
Fix the login bug.
```

Claude does not know which bug, what the expected behavior is, or where to look.

### Good (Specific)

```
The login form on /auth/login returns a 500 error when the email contains a plus sign
(e.g., user+tag@example.com). The issue is likely in the email validation regex in
src/auth/validators.ts. Fix it so plus signs are accepted, and add a test case.
```

### Key Elements of a Specific Prompt

| Element | Why It Matters | Example |
|---------|---------------|---------|
| **What** is the problem | Focuses Claude on the right issue | "500 error on login" |
| **Where** to look | Avoids wasting context searching | "in src/auth/validators.ts" |
| **Expected behavior** | Defines the success condition | "plus signs should be accepted" |
| **Follow-up action** | Ensures completeness | "add a test case" |

---

## 2. Provide Context

Claude Code can read your files, but it does not know your intent unless you state it.

### Techniques for Providing Context

- **Reference files directly:** "Look at `src/config/database.ts` and update the connection pool settings."
- **Describe the architecture:** "This is a Next.js app with a PostgreSQL backend. The API routes are in `app/api/`."
- **Mention constraints:** "We use ESLint with the Airbnb config. Do not disable any lint rules."
- **Link to standards:** "Follow the error handling pattern used in `src/services/userService.ts`."
- **Use CLAUDE.md:** Put recurring context in your project's CLAUDE.md so you do not have to repeat it every session.

---

## 3. Break Down Complex Tasks

If a task involves multiple steps, break it into pieces. Claude handles focused, single-purpose prompts better than sprawling multi-part requests.

### Anti-Pattern: One Giant Prompt

```
Refactor the entire auth module to use JWT instead of sessions, update all the routes,
add refresh token support, update the database schema, write migrations, update all
tests, and update the API documentation.
```

### Better: Step by Step

```
Step 1: Let's plan the migration from sessions to JWT. Use plan mode.
        What files need to change and in what order?

Step 2: Update src/auth/middleware.ts to validate JWTs instead of session cookies.

Step 3: Add a refresh token endpoint at POST /auth/refresh.

Step 4: Write the database migration to add a refresh_tokens table.

Step 5: Update the existing tests in tests/auth/ to use JWT-based auth.
```

---

## 4. Use Plan Mode First

For complex changes, start in plan mode so Claude reads and analyzes before writing.

```
# Start in plan mode
claude --permission-mode plan

> Analyze the payment processing module in src/payments/.
> I want to add Stripe webhook support. What files need to change,
> what new files are needed, and what is the risk of breaking existing
> functionality?
```

After reviewing the plan, switch to default mode and execute:

```
/model default
Now implement the plan you just outlined. Start with the webhook endpoint.
```

---

## 5. When to Use /init vs Manual CLAUDE.md

| Scenario | Use `/init` | Use Manual CLAUDE.md |
|----------|-------------|---------------------|
| New project, first time using Claude Code | Yes | No |
| Existing project with established conventions | Optional | Yes — write your own rules |
| You want Claude to discover the project structure | Yes | No |
| You need strict, opinionated rules | No | Yes — `/init` is generic |
| Onboarding new team members | Yes (as a starting point) | Then customize the output |

**Recommendation:** Run `/init` to generate a baseline, then edit the resulting CLAUDE.md to add your team's specific conventions, anti-patterns, and preferences.

---

## 6. Prompt Templates for Common Tasks

### Refactoring

```
Refactor [file/module] to [goal]. Keep the public API unchanged.
Run the existing tests after refactoring to make sure nothing breaks.
Follow the coding style in [reference file].
```

**Example:**

```
Refactor src/utils/dateHelpers.ts to use date-fns instead of moment.js.
Keep all exported function signatures the same. Run `npm test -- --grep date`
after refactoring. Follow the import style used in src/utils/stringHelpers.ts.
```

### Debugging

```
There is a bug where [symptom]. It started [when/context].
I expect [expected behavior] but instead [actual behavior].
Relevant files: [list]. Check [specific area] first.
```

**Example:**

```
There is a bug where the dashboard shows stale data after a user updates their
profile. It started after the caching PR was merged last week. I expect the
dashboard to reflect changes immediately. Check the cache invalidation logic
in src/cache/invalidator.ts first.
```

### Adding a Feature

```
Add [feature] to [location]. It should [behavior]. Follow the existing
pattern in [similar feature]. Include tests in [test location].
Acceptance criteria: [list].
```

**Example:**

```
Add a "forgot password" flow to the auth module. It should send a reset
email with a time-limited token. Follow the existing pattern in the email
verification flow (src/auth/emailVerification.ts). Include tests in
tests/auth/forgotPassword.test.ts. Acceptance criteria:
1. POST /auth/forgot-password sends an email
2. Token expires after 1 hour
3. POST /auth/reset-password with valid token updates the password
```

### Writing Tests

```
Write tests for [file/function]. Cover: [list of scenarios].
Use [test framework] and follow the style in [existing test file].
Mock [external dependencies].
```

**Example:**

```
Write tests for src/services/orderService.ts. Cover: creating an order,
canceling an order, applying a discount code, and handling out-of-stock items.
Use Jest and follow the style in tests/services/userService.test.ts.
Mock the database calls using the existing test helpers in tests/helpers/db.ts.
```

---

## 7. Anti-Patterns to Avoid

| Anti-Pattern | Why It Fails | Better Alternative |
|-------------|-------------|-------------------|
| "Fix everything" | Too vague, no success criteria | Name the specific bug or behavior |
| "Make it better" | Subjective, no measurable goal | "Reduce function complexity to under 10 lines each" |
| Pasting a full stack trace with no context | Claude needs to know what you expected | Add: "I expected X but got Y" |
| Asking to change 20 files at once | Context window pressure, higher error rate | Break into 3-5 file batches |
| Repeating project rules in every prompt | Wastes tokens and context | Put rules in CLAUDE.md |
| Ignoring plan mode for big changes | Leads to wrong-direction rewrites | Plan first, execute second |
| "Do not change anything else" (over-constraining) | Sometimes related files need updates | "Minimize changes to other files" |
| Not specifying the test command | Claude may guess wrong | "Run `npm test` after changes" |

---

## 8. Advanced Prompting Techniques

### Chaining with /compact

For long sessions, use `/compact` with a focus topic to preserve the most important context:

```
/compact focus on the database migration we just planned
```

### Using Examples in Prompts

```
Add a new API endpoint following this pattern:

// Existing example (GET /users):
router.get('/users', authenticate, async (req, res) => {
  const users = await userService.getAll(req.query);
  res.json({ data: users });
});

// Create a similar endpoint for GET /orders
```

### Referencing Git History

```
Look at the last 5 commits on this branch. There is a regression in the
search functionality. Find which commit introduced it and fix it.
```

---

## Navigation

| Direction | Link |
|-----------|------|
| Previous Lesson | [Keyboard Shortcuts Reference](keyboard-shortcuts-reference.md) |
| Next Lesson | [Troubleshooting Guide](troubleshooting-guide.md) |
| Module Overview | [Module 11: Cheat Sheets](README.md) |

---

> **Tip:** The best prompt is the one that gives Claude enough context to succeed on the first try. Spending 30 extra seconds writing a clear prompt saves minutes of back-and-forth.
