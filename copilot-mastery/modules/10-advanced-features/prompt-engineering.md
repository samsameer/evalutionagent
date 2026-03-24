# Prompt Engineering for Copilot

**Module 10, Lesson 5 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Prompt engineering is the art of crafting instructions that get the best possible results from AI models. While Copilot is powerful out of the box, knowing how to communicate effectively with it can dramatically improve output quality.

---

## The Five Principles of Effective Copilot Prompts

### 1. Be Specific, Not Vague

```
❌ BAD:  "Make this better"
✅ GOOD: "Refactor this function to use early returns instead of nested
         if-else blocks, and add TypeScript strict null checks"

❌ BAD:  "Fix the bug"
✅ GOOD: "Fix the bug where getUserById returns null instead of throwing
         a NotFoundError when the user doesn't exist in the database"

❌ BAD:  "Add tests"
✅ GOOD: "Add Jest unit tests covering: valid input, empty string input,
         null input, and input exceeding 255 characters"
```

### 2. Provide Context

```
❌ BAD:  "Create a login form"
✅ GOOD: "Create a login form React component using our existing design
         system. Use the Input component from #file:src/components/Input.tsx
         and the Button from #file:src/components/Button.tsx. The form
         should call the auth API at /api/auth/login."
```

### 3. Specify the Output Format

```
❌ BAD:  "Explain this code"
✅ GOOD: "Explain this code in 3 sections:
         1. What it does (2-3 sentences)
         2. How it works (step-by-step)
         3. Potential issues or edge cases"
```

### 4. Reference Existing Patterns

```
✅ GOOD: "Create a new service following the same pattern as
         #file:src/services/user.service.ts — same class structure,
         same error handling, same dependency injection approach"
```

### 5. Constrain When Necessary

```
✅ GOOD: "Implement this using only the standard library — no external
         packages. The solution should handle up to 1 million records
         without running out of memory."
```

---

## Prompt Patterns for Common Tasks

### The Scaffold Pattern

```
Create a [thing] with the following structure:
- [Component 1] — [description]
- [Component 2] — [description]
- [Component 3] — [description]

Use [technology/pattern] and follow the conventions in [reference file].
Include tests for [specific scenarios].
```

### The Fix Pattern

```
There is a bug in #file:[path]:

**Expected behavior:** [what should happen]
**Actual behavior:** [what happens instead]
**Steps to reproduce:** [how to trigger the bug]

Fix the bug and add a regression test.
```

### The Refactor Pattern

```
Refactor #selection to:
1. [Specific improvement 1]
2. [Specific improvement 2]
3. [Specific improvement 3]

Keep the same public API — no breaking changes to callers.
Add tests to verify behavior is unchanged.
```

### The Explain Pattern

```
Explain this code as if I'm a [junior/senior] developer.
Focus on:
- Why this approach was chosen
- What trade-offs were made
- What could go wrong
```

---

## Prompt Engineering for Inline Completions

For better inline completions (ghost text), engineer your **code context**:

### Write Intent Comments

```python
# Calculate the cosine similarity between two vectors
# using numpy for efficient computation
def cosine_similarity(vec_a, vec_b):
    # Copilot now generates the implementation with numpy
```

### Use Descriptive Names

```typescript
// Good names give Copilot clear intent
function fetchPaginatedUsersWithFilters(
  page: number,
  pageSize: number,
  filters: UserFilter
): Promise<PaginatedResponse<User>> {
  // Copilot understands exactly what to implement
```

### Provide Type Annotations

```typescript
// Rich types = better completions
interface CreateOrderRequest {
  customerId: string;
  items: Array<{ productId: string; quantity: number }>;
  shippingAddress: Address;
  paymentMethod: PaymentMethod;
  couponCode?: string;
}

function createOrder(request: CreateOrderRequest): Promise<Order> {
  // Copilot generates accurate implementation based on types
```

---

## Anti-Patterns to Avoid

| Anti-Pattern | Why It is Bad | Better Approach |
|-------------|--------------|----------------|
| "Do everything" | Overwhelms the model | Break into smaller tasks |
| No context | Model guesses your intent | Provide files, examples, constraints |
| Overly long prompts | Key instructions get lost | Be concise, put important info first |
| Contradictory instructions | Confuses the model | Review for consistency |
| Not reviewing output | AI makes mistakes | Always verify generated code |

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 10: Advanced Features](README.md) |
| Previous Lesson | [Knowledge Bases](knowledge-bases.md) |
| Next Module | [Module 11: Security, Privacy & Admin](../11-security-privacy-admin/) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
