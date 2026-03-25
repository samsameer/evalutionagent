# Hook Recipes

**Claude Code Mastery — March 2026**
**Instructor: Jabbir Basha, Principal AI Engineer**

---

Hooks are configured in `.claude/settings.json` under the `hooks` key. Each hook specifies a lifecycle event and a shell command to run.

## Recipe 1: Auto-Lint on File Write

```json
{ "hooks": { "postToolUse": [
  { "matcher": "write|edit", "command": "npx eslint --fix \"$CLAUDE_FILE_PATH\" 2>/dev/null || true" }
] } }
```

## Recipe 2: Auto-Format with Prettier

```json
{ "hooks": { "postToolUse": [
  { "matcher": "write|edit", "command": "npx prettier --write \"$CLAUDE_FILE_PATH\" 2>/dev/null || true" }
] } }
```

## Recipe 3: Desktop Notification on Task Complete

```json
{ "hooks": { "notification": [
  { "matcher": ".*", "command": "notify-send 'Claude Code' \"$CLAUDE_NOTIFICATION_MESSAGE\" 2>/dev/null || osascript -e 'display notification \"'\"$CLAUDE_NOTIFICATION_MESSAGE\"'\" with title \"Claude Code\"' 2>/dev/null || true" }
] } }
```

## Recipe 4: Log All Tool Usage

```json
{ "hooks": { "preToolUse": [
  { "matcher": ".*", "command": "echo \"$(date -u +%Y-%m-%dT%H:%M:%SZ) | Tool: $CLAUDE_TOOL_NAME | Input: $CLAUDE_TOOL_INPUT\" >> ~/.claude/tool-usage.log" }
] } }
```

## Recipe 5: Block Dangerous Commands

```json
{ "hooks": { "preToolUse": [
  { "matcher": "bash", "command": "if echo \"$CLAUDE_TOOL_INPUT\" | grep -qE 'rm -rf /|mkfs|dd if=|:(){ :|:& };:|shutdown|reboot'; then echo 'BLOCKED' >&2; exit 1; fi" }
] } }
```

## Recipe 6: Auto-Run Tests After Code Changes

```json
{ "hooks": { "postToolUse": [
  { "matcher": "write|edit", "command": "if echo \"$CLAUDE_FILE_PATH\" | grep -qE '\\.(ts|js|py)$' && ! echo \"$CLAUDE_FILE_PATH\" | grep -q 'test'; then npm test --silent 2>/dev/null || true; fi" }
] } }
```

## Recipe 7: Python Auto-Format with Ruff

```json
{ "hooks": { "postToolUse": [
  { "matcher": "write|edit", "command": "if echo \"$CLAUDE_FILE_PATH\" | grep -qE '\\.py$'; then ruff format \"$CLAUDE_FILE_PATH\" && ruff check --fix \"$CLAUDE_FILE_PATH\" 2>/dev/null || true; fi" }
] } }
```

## Recipe 8: Git Auto-Stage Modified Files

```json
{ "hooks": { "postToolUse": [
  { "matcher": "write|edit", "command": "git add \"$CLAUDE_FILE_PATH\" 2>/dev/null || true" }
] } }
```

## Recipe 9: Enforce File Size Limits

```json
{ "hooks": { "postToolUse": [
  { "matcher": "write", "command": "if [ -f \"$CLAUDE_FILE_PATH\" ] && [ $(wc -l < \"$CLAUDE_FILE_PATH\") -gt 500 ]; then echo 'WARNING: File exceeds 500 lines.' >&2; fi" }
] } }
```

## Recipe 10: Sound Alert on Completion

```json
{ "hooks": { "notification": [
  { "matcher": ".*", "command": "afplay /System/Library/Sounds/Glass.aiff 2>/dev/null || paplay /usr/share/sounds/freedesktop/stereo/complete.oga 2>/dev/null || true" }
] } }
```

## Combining Multiple Hooks

You can chain multiple hooks for the same event. They run in declared order.

```json
{
  "hooks": {
    "postToolUse": [
      { "matcher": "write|edit", "command": "npx prettier --write \"$CLAUDE_FILE_PATH\" 2>/dev/null || true" },
      { "matcher": "write|edit", "command": "npx eslint --fix \"$CLAUDE_FILE_PATH\" 2>/dev/null || true" },
      { "matcher": "write|edit", "command": "git add \"$CLAUDE_FILE_PATH\" 2>/dev/null || true" }
    ],
    "preToolUse": [
      { "matcher": "bash", "command": "if echo \"$CLAUDE_TOOL_INPUT\" | grep -qE 'rm -rf /'; then exit 1; fi" }
    ]
  }
}
```

---

> **Note:** Hook commands that exit with a non-zero status code on `preToolUse` will block the tool from executing. Use `|| true` on post-hooks to prevent false failures from interrupting Claude.
