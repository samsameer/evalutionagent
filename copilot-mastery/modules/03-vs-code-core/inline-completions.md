# Inline Completions & Ghost Text

**Module 03, Lesson 1 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Inline completions are the **bread and butter** of GitHub Copilot. As you type code, Copilot displays suggestions as semi-transparent "ghost text" directly in your editor. This lesson covers everything about how to work with these suggestions effectively.

---

## How Ghost Text Works

When you type code in a Copilot-enabled file, the AI analyzes your context and generates a suggestion. This appears as **gray, semi-transparent text** after your cursor.

### Example: Writing a Python Function

You type:
```python
def calculate_distance(lat1, lon1, lat2, lon2):
    """Calculate the distance between two GPS coordinates using the Haversine formula."""
```

Copilot suggests (in ghost text):
```python
    from math import radians, cos, sin, asin, sqrt

    lat1, lon1, lat2, lon2 = map(radians, [lat1, lon1, lat2, lon2])
    dlat = lat2 - lat1
    dlon = lon2 - lon1
    a = sin(dlat/2)**2 + cos(lat1) * cos(lat2) * sin(dlon/2)**2
    c = 2 * asin(sqrt(a))
    r = 6371  # Radius of Earth in kilometers
    return c * r
```

---

## Accepting Suggestions

### Full Accept

Press **Tab** to accept the entire suggestion.

### Partial Accept (Word by Word)

Press **Ctrl+Right Arrow** (Windows/Linux) or **Cmd+Right Arrow** (macOS) to accept one word at a time. This is incredibly useful when:

- The first part of the suggestion is correct but the rest needs changes
- You want to accept a variable name but modify the value
- The suggestion is mostly right but you want to diverge midway

### Partial Accept (Line by Line)

Press **Ctrl+Right Arrow** at the end of a line to accept just the current line of a multi-line suggestion, then continue to the next.

### Dismiss

Press **Escape** to dismiss the current suggestion entirely.

---

## Keyboard Shortcuts for Completions

| Action | Windows/Linux | macOS |
|--------|--------------|-------|
| Accept full suggestion | `Tab` | `Tab` |
| Accept next word | `Ctrl+Right Arrow` | `Cmd+Right Arrow` |
| Dismiss suggestion | `Escape` | `Escape` |
| Show next suggestion | `Alt+]` | `Option+]` |
| Show previous suggestion | `Alt+[` | `Option+[` |
| Trigger suggestion manually | `Alt+\` | `Option+\` |
| Open completions panel | `Ctrl+Shift+Alt+]` | Not available |

---

## Types of Completions

### 1. Single-Line Completions

Copilot completes the current line based on context:

```javascript
// You type:
const userEmail = user.

// Copilot suggests:
email.toLowerCase().trim()
```

### 2. Multi-Line Completions

Copilot generates entire code blocks — functions, loops, conditionals:

```typescript
// You type:
function validateEmail(email: string): boolean {

// Copilot suggests:
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  return emailRegex.test(email);
}
```

### 3. Comment-Driven Completions

Write a comment describing what you want, and Copilot generates the code:

```python
# Sort a list of dictionaries by the 'age' key in descending order

# Copilot suggests:
sorted_list = sorted(data, key=lambda x: x['age'], reverse=True)
```

### 4. Fill-in-the-Middle (FIM)

Copilot can suggest code to fill in the middle of existing code — not just at the end of a line. If you place your cursor between existing code, Copilot understands the surrounding context and suggests appropriate code to bridge the gap.

---

## Tips for Better Completions

### 1. Write Descriptive Comments First

```python
# BAD: No context
def process():

# GOOD: Clear intent
def process_customer_order(order_id: str, items: list[dict]) -> dict:
    """Process a customer order by validating items, calculating total, and applying discounts."""
```

### 2. Use Descriptive Variable and Function Names

```javascript
// BAD: Copilot has no context
const x = getData();

// GOOD: Copilot understands intent
const activeSubscribers = fetchActiveSubscribersFromDatabase();
```

### 3. Keep Related Files Open

Copilot uses open tabs as context. If you are implementing an interface, keep the interface file open in another tab.

### 4. Type the Function Signature First

```typescript
// Type the signature with types:
function mergeArrays<T>(arr1: T[], arr2: T[], comparator: (a: T, b: T) => boolean): T[] {

// Copilot now has clear intent and types to work with
```

### 5. Provide Example Data

```python
# Sample input: [{"name": "Alice", "score": 95}, {"name": "Bob", "score": 87}]
# Expected output: {"Alice": "A", "Bob": "B+"}
def assign_grades(students):
```

---

## Understanding When Copilot Triggers

Copilot generates suggestions when:

- You **pause typing** for a brief moment (configurable delay)
- You **start a new line** after a function signature, comment, or statement
- You **type a trigger character** like `(`, `.`, `{`, or `=`
- You **manually trigger** with `Alt+\` or `Option+\`

Copilot does NOT trigger when:

- You are in a read-only file
- The file type is disabled in settings
- You are in a commit message editor (unless enabled)
- Network connectivity is lost

---

## Completions in Different Languages

Copilot works with virtually every programming language. Here is a quality comparison based on training data availability:

| Tier | Languages | Completion Quality |
|------|----------|-------------------|
| **Tier 1** (Best) | Python, JavaScript, TypeScript, Java, C#, Go, Rust | Excellent — deep understanding of idioms and patterns |
| **Tier 2** (Great) | Ruby, PHP, Swift, Kotlin, C++, Scala, Dart | Very good — handles most patterns well |
| **Tier 3** (Good) | R, Julia, Lua, Haskell, Elixir, Perl | Good — may need more guidance via comments |
| **Tier 4** (Decent) | Assembly, COBOL, Fortran, VHDL | Basic — works but may need significant guidance |

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 03: VS Code Core](README.md) |
| Next Lesson | [Next Edit Suggestions (NES)](next-edit-suggestions.md) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
