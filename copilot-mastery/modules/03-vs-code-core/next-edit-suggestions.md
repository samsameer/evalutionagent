# Next Edit Suggestions (NES)

**Module 03, Lesson 2 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Next Edit Suggestions (NES) is one of the most revolutionary Copilot features released in 2025-2026. Instead of just suggesting code where your cursor is, NES **predicts where you need to edit next** and proactively offers the change — even in different parts of the file.

---

## What Are Next Edit Suggestions?

Traditional Copilot: You type → Copilot suggests at cursor position.

**NES**: You make a change → Copilot identifies other places in your file that need a **related change** and highlights them with a suggestion.

### Real-World Example

Imagine you rename a parameter from `userId` to `accountId` in a function signature:

```typescript
// Before: You change this line
function getUser(userId: string) {

// After your change:
function getUser(accountId: string) {
```

**NES immediately suggests** updating all references to `userId` inside the function body:

```typescript
// NES highlights this line and suggests:
// Before: const user = await db.users.findById(userId);
// NES suggestion: const user = await db.users.findById(accountId);
```

You press **Tab** to accept the suggestion, and NES jumps to the **next location** that needs updating. It is like having an intelligent find-and-replace that understands code semantics.

---

## How NES Differs from Regular Completions

| Feature | Regular Completions | Next Edit Suggestions |
|---------|-------------------|----------------------|
| Trigger | You type new code | You edit existing code |
| Location | At your cursor | Anywhere in the file |
| Purpose | Generate new code | Update related code |
| Navigation | Stay at cursor | Jumps to next edit location |
| Icon | Ghost text | Highlighted with arrow indicator |

---

## How to Use NES

### Step 1: Make an Edit

Change something in your code — rename a variable, update a type, modify a parameter, change a value.

### Step 2: Look for the NES Indicator

After your edit, look for:
- A **lightbulb or arrow icon** in the gutter (left margin)
- **Highlighted code** elsewhere in the file with a suggested change
- A **decorative marker** showing where the next edit should go

### Step 3: Accept or Navigate

| Action | Shortcut |
|--------|----------|
| Accept NES suggestion | `Tab` |
| Jump to next NES location | `Tab` (after accepting) |
| Dismiss NES suggestion | `Escape` |
| Skip to next NES suggestion | `Alt+]` / `Option+]` |

### Step 4: Repeat

After accepting one NES suggestion, Copilot may immediately show the **next related edit** elsewhere in the file. Keep pressing Tab to cascade through all related changes.

---

## Common NES Scenarios

### 1. Variable Renaming

```python
# You change:
def calculate(price):  # Changed from 'amount' to 'price'

# NES suggests updating all occurrences:
    tax = price * 0.1        # Was: amount * 0.1
    total = price + tax       # Was: amount + tax
    return total
```

### 2. Type Changes

```typescript
// You change the return type:
function getItems(): Promise<Item[]> {  // Changed from Item[] to Promise<Item[]>

// NES suggests:
    const items = await fetchItems();  // Adds 'await'
    return items;
}
```

### 3. Function Signature Updates

```java
// You add a new parameter:
public void sendEmail(String to, String subject, String cc) {  // Added 'cc'

// NES suggests adding cc to the email builder:
    EmailBuilder builder = new EmailBuilder()
        .setTo(to)
        .setSubject(subject)
        .setCc(cc);  // NES adds this line
```

### 4. Pattern Replication

```javascript
// You add error handling to one function:
async function getUser(id) {
  try {
    return await api.get(`/users/${id}`);
  } catch (error) {
    logger.error('Failed to get user', error);
    throw error;
  }
}

// NES suggests the same pattern for similar functions below:
async function getOrder(id) {
  // NES suggests wrapping in try/catch with the same pattern
```

---

## Enabling NES

NES is enabled by default in VS Code 1.95+ with the latest Copilot extension. To verify or toggle:

1. Open Settings (`Ctrl+,` / `Cmd+,`)
2. Search for **"Copilot next edit"**
3. Ensure `github.copilot.nextEditSuggestions.enabled` is checked

```json
{
  "github.copilot.nextEditSuggestions.enabled": true
}
```

---

## Tips for Getting the Most from NES

1. **Make clean, intentional edits** — NES works best when your edit has a clear pattern
2. **Work in well-typed languages** — TypeScript, Java, C# give NES more context
3. **Keep files focused** — Smaller, focused files help NES identify related changes
4. **Accept sequentially** — After accepting one NES, wait briefly for the next one
5. **Do not fight it** — If NES suggests something wrong, dismiss and edit manually

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 03: VS Code Core](README.md) |
| Previous Lesson | [Inline Completions](inline-completions.md) |
| Next Lesson | [Completions Panel & Navigation](completions-panel.md) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
