# Copilot Edits — Multi-File Editing

**Module 05, Lesson 1 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Copilot Edits allows you to make changes across **multiple files** in a single editing session using natural language. Unlike inline chat (which edits one location), Copilot Edits understands the broader context of your request and modifies all relevant files simultaneously, showing you a diff of every change before applying.

---

## How to Start a Copilot Edits Session

### Method 1: Chat Panel Edit Mode

1. Open the Chat Panel (`Ctrl+Alt+I` / `Cmd+Option+I`)
2. Click the **mode selector** at the top
3. Select **"Edit"** mode
4. Add files to the working set (files Copilot can edit)
5. Type your editing request
6. Review the diffs and accept or reject each change

### Method 2: Command Palette

1. Press `Ctrl+Shift+P` / `Cmd+Shift+P`
2. Type **"Copilot Edits: Start Edit Session"**
3. Follow the same flow

---

## The Working Set

The **working set** is the list of files that Copilot Edits can modify. You control exactly which files are included.

### Adding Files to the Working Set

| Method | How |
|--------|-----|
| Click "Add Files" button | In the Edits panel, click the + icon |
| Drag from Explorer | Drag files from the file explorer into the edit panel |
| Use #file reference | Type `#file:path/to/file.ts` in your message |
| Open files | All currently open editor tabs can be added |

### Why the Working Set Matters

- Copilot only modifies files **in the working set**
- Adding more relevant files gives Copilot better context
- Limiting the working set prevents unintended changes
- You should include files that are **relevant to your task**

---

## Example: Adding Authentication to an API

### Your Request:
```
Add JWT authentication middleware to all API routes.
The middleware should:
- Verify the JWT token from the Authorization header
- Attach the decoded user to the request object
- Return 401 for invalid or missing tokens
- Skip authentication for /api/auth/login and /api/auth/register
```

### Working Set:
- `src/middleware/auth.middleware.ts` (new file)
- `src/routes/index.ts`
- `src/routes/users.ts`
- `src/routes/orders.ts`
- `src/types/express.d.ts`

### What Copilot Edits Does:

1. **Creates** `auth.middleware.ts` with the JWT verification logic
2. **Modifies** `routes/index.ts` to apply the middleware globally
3. **Updates** `routes/users.ts` and `routes/orders.ts` to use the authenticated user
4. **Updates** `express.d.ts` to extend the Request type with the user property

Each change is shown as a **diff** that you can:
- **Accept** (apply the change)
- **Reject** (keep the original)
- **Modify** (edit the suggestion before accepting)

---

## Reviewing Diffs

When Copilot Edits proposes changes, you see a **diff view** for each file:

```diff
// src/middleware/auth.middleware.ts (NEW FILE)
+ import jwt from 'jsonwebtoken';
+ import { Request, Response, NextFunction } from 'express';
+
+ const PUBLIC_ROUTES = ['/api/auth/login', '/api/auth/register'];
+
+ export function authMiddleware(req: Request, res: Response, next: NextFunction) {
+   if (PUBLIC_ROUTES.includes(req.path)) {
+     return next();
+   }
+
+   const token = req.headers.authorization?.split(' ')[1];
+   if (!token) {
+     return res.status(401).json({ error: 'No token provided' });
+   }
+
+   try {
+     const decoded = jwt.verify(token, process.env.JWT_SECRET!);
+     req.user = decoded;
+     next();
+   } catch (error) {
+     return res.status(401).json({ error: 'Invalid token' });
+   }
+ }
```

### Diff Actions

| Action | Description |
|--------|-------------|
| **Accept** | Apply this change to the file |
| **Reject** | Discard this change |
| **Accept All** | Apply all proposed changes across all files |
| **Reject All** | Discard all proposed changes |

---

## Tips for Effective Edits

1. **Be specific** about what you want changed and how
2. **Include all relevant files** in the working set
3. **Review every diff** before accepting — Copilot is good but not perfect
4. **Use iterative edits** — start with a broad change, then refine
5. **Undo if needed** — `Ctrl+Z` / `Cmd+Z` works on accepted edits

---

## Copilot Edits vs. Inline Chat vs. Agent Mode

| Feature | Inline Chat | Copilot Edits | Agent Mode |
|---------|------------|---------------|------------|
| Scope | Single location | Multiple files | Entire project |
| User control | High | High (review diffs) | Lower (autonomous) |
| Terminal access | No | No | Yes |
| Creates files | No | Yes | Yes |
| Installs packages | No | No | Yes |
| Self-corrects | No | No | Yes |
| Best for | Quick fixes | Planned changes | Complex tasks |

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 05: Edits & Agent Mode](README.md) |
| Next Lesson | [Agent Mode — Autonomous Coding](agent-mode.md) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
