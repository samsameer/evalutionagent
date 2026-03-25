# Headless & Non-Interactive Mode

**Module 07, Lesson 5 — Claude Code Mastery**

**Instructor: Jabbir Basha, Principal AI Engineer**

---

## Overview

Claude Code's headless mode lets you run it as a non-interactive command-line tool. Using the `-p` (print) flag, you can pipe prompts in, get structured output back, and integrate Claude into scripts, CI/CD pipelines, and automated workflows. This lesson covers output formats, control flags, and practical integration patterns.

---

## Print Mode with -p

The `-p` flag runs Claude Code in print mode. It accepts a prompt, processes it, and outputs the result to stdout:

```bash
claude -p "Explain what the main function in src/index.ts does"
```

Print mode is non-interactive — Claude processes the request and exits. There is no conversation history and no follow-up.

---

## Output Formats

Control output with the `--output-format` flag:

| Format | Flag | Use Case |
|--------|------|----------|
| Plain text | `--output-format text` | Human-readable output (default) |
| JSON | `--output-format json` | Structured parsing in scripts |
| Streaming JSON | `--output-format stream-json` | Real-time processing of partial results |

**Text** returns plain output with no metadata. **JSON** returns a structured object with `result`, `cost`, `input_tokens`, `output_tokens`, and `duration_ms` fields — ideal for script parsing. **Stream-JSON** emits newline-delimited JSON objects as the response generates, useful for progress indicators.

```bash
claude -p "Summarize the README" --output-format text
claude -p "List exported functions" --output-format json | jq '.result'
claude -p "Refactor this function" --output-format stream-json
```

---

## Piping Input and Output

Claude Code reads from stdin when input is piped:

```bash
# Pipe file contents as context
cat src/auth/middleware.ts | claude -p "Review this code for security issues"

# Chain with other tools
git diff HEAD~1 | claude -p "Write a commit message for these changes"

# Process output with jq
claude -p "List the API endpoints" --output-format json | jq '.result'
```

You can combine stdin input with a prompt — the piped content becomes additional context for the prompt.

---

## Control Flags

### --max-turns

Limit how many agent turns Claude can take:

```bash
claude -p "Fix the failing tests" --max-turns 5
```

This prevents runaway sessions in automation. If Claude cannot complete the task within the turn limit, it returns what it has so far.

### --allowedTools and --denyTools

Control which tools Claude can use:

```bash
# Only allow file reading and searching
claude -p "Find all TODO comments" --allowedTools Read,Grep,Glob

# Allow everything except file writing
claude -p "Analyze the codebase" --denyTools Write,Edit
```

Use `--allowedTools` for strict whitelisting in sensitive environments. Use `--denyTools` to block specific dangerous operations while allowing everything else.

### --system-prompt and --append-system-prompt

Inject custom instructions:

```bash
# Replace the default system prompt
claude -p "Review this PR" --system-prompt "You are a security auditor. Focus only on vulnerabilities."

# Add to the default system prompt
claude -p "Review this PR" --append-system-prompt "Always check for SQL injection and XSS."
```

`--system-prompt` replaces the entire system prompt. `--append-system-prompt` adds to it. In most cases, appending is safer since it preserves Claude Code's built-in capabilities.

---

## CI/CD Integration Examples

### Pull Request Review

```bash
#!/bin/bash
gh pr diff "$PR_NUMBER" | claude -p "Review this diff. Flag bugs and security issues." \
  --output-format text --max-turns 3 --denyTools Write,Edit,Bash \
  | gh pr comment "$PR_NUMBER" --body-file -
```

### Automated Test Analysis

```bash
#!/bin/bash
npm test 2>&1 | claude -p "Analyze these test failures and suggest fixes." \
  --output-format json --max-turns 5 | jq '.result'
```

---

## Scripting Patterns

### Batch Processing

```bash
#!/bin/bash
for file in src/components/*.tsx; do
  claude -p "Add JSDoc comments to all exported functions in $file" \
    --allowedTools Read,Edit --max-turns 3
done
```

### Conditional Logic with JSON Output

```bash
#!/bin/bash
RESULT=$(claude -p "Does src/config.ts have any hardcoded secrets?" --output-format json)
if echo "$RESULT" | jq -r '.result' | grep -qi "found\|hardcoded"; then
  echo "WARNING: Potential secrets detected" && exit 1
fi
```

---

## GitHub Actions Usage

```yaml
name: Claude Code Review
on: [pull_request]
jobs:
  review:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm install -g @anthropic-ai/claude-code
      - name: Review and comment
        env:
          ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
          GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        run: |
          gh pr diff ${{ github.event.pull_request.number }} | \
          claude -p "Review this diff for bugs and security issues." \
            --output-format text --max-turns 3 --denyTools Write,Edit,Bash | \
          gh pr comment ${{ github.event.pull_request.number }} --body-file -
```

---

## Summary

Headless mode with `-p` turns Claude Code into a scriptable CLI tool. Use `--output-format` for structured output, `--max-turns` to bound execution, and `--allowedTools`/`--denyTools` for safety. Combine with `--system-prompt` or `--append-system-prompt` to customize behavior for specific automation tasks. These capabilities make Claude Code a first-class citizen in CI/CD pipelines, batch scripts, and GitHub Actions workflows.

---

[← Back to Module Overview](README.md)

[← Previous Module](../06-hooks-mcp-commands/) | [Course Home](../../README.md) | [Next Module →](../08-multi-platform/)
