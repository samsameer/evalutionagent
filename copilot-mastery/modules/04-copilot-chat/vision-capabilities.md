# Vision & Image Understanding

**Module 04, Lesson 4 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Copilot Chat can **understand images** — including screenshots, UI mockups, architecture diagrams, and error screenshots. This vision capability leverages multimodal AI models to bridge the gap between visual design and code.

---

## What Vision Can Do

| Use Case | Example |
|----------|---------|
| **UI Implementation** | Paste a Figma screenshot → Get React/HTML/CSS code |
| **Error Debugging** | Screenshot an error dialog → Get a fix |
| **Diagram to Code** | Share an architecture diagram → Get implementation guidance |
| **Design Review** | Paste a UI screenshot → Get accessibility feedback |
| **Documentation** | Screenshot a whiteboard → Get structured notes |

---

## How to Use Vision in Copilot Chat

### Method 1: Paste an Image

1. Copy an image to your clipboard (screenshot, snip, etc.)
2. Open Copilot Chat panel
3. Paste the image directly into the chat input (`Ctrl+V` / `Cmd+V`)
4. Type your question alongside the image
5. Press Enter

### Method 2: Drag and Drop

1. Drag an image file from your file explorer
2. Drop it into the Copilot Chat input area
3. Type your question
4. Press Enter

### Method 3: Attach from File

1. Click the **attachment icon** (paperclip) in the chat input
2. Select an image file from your workspace or filesystem
3. Type your question
4. Press Enter

---

## Practical Examples

### Example 1: UI Screenshot to Code

```
[Paste screenshot of a login form]

"Convert this login form design into a React component using Tailwind CSS.
Include form validation and error states."
```

Copilot generates:
- Complete React component
- Tailwind CSS classes matching the design
- Form validation logic
- Error state handling

### Example 2: Error Screenshot to Fix

```
[Paste screenshot of a browser console error]

"What's causing this error and how do I fix it?"
```

Copilot:
- Reads the error message from the image
- Identifies the root cause
- Provides a code fix

### Example 3: Architecture Diagram to Implementation

```
[Paste a system architecture diagram]

"Based on this architecture, create the folder structure and
initial service files for the microservices shown."
```

### Example 4: Whiteboard to User Stories

```
[Paste photo of a whiteboard with feature notes]

"Convert these whiteboard notes into structured user stories
with acceptance criteria."
```

---

## Supported Models for Vision

Not all models in Copilot support vision. Here is the support matrix:

| Model | Vision Support |
|-------|---------------|
| GPT-4o | Yes |
| Claude 3.5 Sonnet | Yes |
| Claude 3.7 Sonnet | Yes |
| Gemini 2.0 Flash | Yes |
| Gemini 2.5 Pro | Yes |
| o1 | Limited |
| o3-mini | No |

> **Tip:** For best vision results, use **GPT-4o** or **Claude 3.5 Sonnet** which have excellent image understanding.

---

## Tips for Better Vision Results

1. **Use clear, high-resolution images** — Blurry or low-resolution images produce worse results
2. **Crop to relevant content** — Remove unnecessary UI elements around the area of interest
3. **Be specific in your prompt** — "Generate this UI" is vague. "Convert this login form to a React component with Tailwind CSS" is actionable
4. **Annotate if needed** — Circle or highlight the relevant parts of complex diagrams
5. **Combine with code context** — Reference your existing files alongside the image

---

## Supported Image Formats

| Format | Supported |
|--------|-----------|
| PNG | Yes |
| JPEG / JPG | Yes |
| GIF | Yes (first frame) |
| WebP | Yes |
| SVG | Partial (rasterized) |
| PDF | No (use text extraction instead) |

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 04: Copilot Chat](README.md) |
| Previous Lesson | [Context Variables & References](context-variables.md) |
| Next Module | [Module 05: Copilot Edits & Agent Mode](../05-copilot-edits-agent-mode/) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
