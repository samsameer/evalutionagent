# Git Integration

**Module 05, Lesson 3 — Claude Code Mastery**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

Claude Code treats Git as a first-class workflow. It can create commits with meaningful messages, manage branches, open pull requests, and even run parallel development sessions using worktrees — all from natural language prompts. This lesson covers every Git capability and the safety rules that keep your repository safe.

---

## Creating Commits

When you ask Claude to commit, it follows a strict protocol:

1. Runs `git status` and `git diff` to understand all changes
2. Reads recent commit messages to match the repository's style
3. Drafts a concise commit message focused on the **why**, not the what
4. Stages only the relevant files (never blindly runs `git add -A`)
5. Creates the commit and verifies success with `git status`

**Example prompt:**

```
Commit these changes with an appropriate message.
```

**What Claude does internally:**

```bash
# Step 1: Inspect changes
git status
git diff --staged
git diff
git log --oneline -10

# Step 2: Stage specific files
git add src/auth/login.ts src/auth/login.test.ts

# Step 3: Commit with a HEREDOC message
git commit -m "$(cat <<'EOF'
Fix login redirect loop when session token is expired

The redirect check was comparing against the raw token instead of
the decoded expiry timestamp, causing an infinite loop.
EOF
)"
```

### Commit Message Style

| Aspect | Rule |
|--------|------|
| Length | 1-2 sentences for the summary line |
| Focus | Explain **why** the change was made |
| Verb | Use imperative mood ("Fix", "Add", "Update") |
| Context | Match the repo's existing commit style |
| Secrets | Never commit `.env`, credentials, or API keys |

---

## Creating Branches

Claude can create and switch branches as part of any workflow:

```
Create a new branch called feature/add-oauth and start working on OAuth integration.
```

Claude will run:

```bash
git checkout -b feature/add-oauth
```

For feature work, Claude typically creates the branch first, makes all changes, then commits — keeping `main` clean.

---

## Creating Pull Requests

Claude uses the GitHub CLI (`gh`) to create pull requests. The workflow:

1. Checks if the branch is pushed to the remote
2. Runs `git log` and `git diff main...HEAD` to understand all commits
3. Pushes with `-u` flag if needed
4. Creates the PR with a structured body

**Example prompt:**

```
Create a pull request for this branch.
```

**What Claude generates:**

```bash
gh pr create --title "Add OAuth 2.0 login flow" --body "$(cat <<'EOF'
## Summary
- Add OAuth 2.0 authorization code flow with PKCE
- Integrate with Google and GitHub identity providers
- Add session management with refresh token rotation

## Test plan
- [ ] Verify login redirect to OAuth provider
- [ ] Verify callback handles tokens correctly
- [ ] Verify refresh token rotation on expiry
- [ ] Test with both Google and GitHub providers
EOF
)"
```

### Resuming from PRs

You can start a Claude session from an existing PR:

```bash
claude --from-pr 142
```

Claude reads the PR description, the diff, and all review comments, then picks up where the conversation left off. This is powerful for addressing code review feedback.

---

## Worktrees for Parallel Development

The `--worktree` flag lets Claude work in an isolated Git worktree, so you can keep using your main working directory while Claude works in parallel.

```bash
claude --worktree "Refactor the auth module to use the new token format"
```

**How it works:**

| Step | What Happens |
|------|--------------|
| 1 | Claude creates a new Git worktree in a temporary directory |
| 2 | A new branch is created for the worktree |
| 3 | Claude makes all changes in the isolated worktree |
| 4 | You continue working in your original directory |
| 5 | When done, Claude can create a PR from the worktree branch |

**Benefits:**

- No conflicts with your current work
- Multiple Claude sessions can run in parallel on different tasks
- Each worktree has its own branch and working directory
- Perfect for handling multiple code review items simultaneously

---

## Git Safety Rules

Claude follows strict safety rules to protect your repository:

| Rule | Description |
|------|-------------|
| **Never force push** | `git push --force` is never used unless you explicitly ask |
| **Never skip hooks** | `--no-verify` is never passed to commits or pushes |
| **Never amend without asking** | `git commit --amend` only when you explicitly request it |
| **New commits after hook failures** | If a pre-commit hook fails, Claude fixes the issue and creates a **new** commit |
| **No destructive resets** | `git reset --hard`, `git checkout .`, `git clean -f` require explicit permission |
| **No force push to main** | Claude warns you if you ask to force push to main or master |
| **Specific file staging** | Prefers `git add <file>` over `git add -A` to avoid accidental inclusions |
| **No interactive flags** | Never uses `-i` flags (e.g., `git rebase -i`) since they require interactive input |

### What Happens When a Pre-Commit Hook Fails

This is a critical detail. When a hook fails:

1. The commit did **not** happen
2. Claude fixes the linting or formatting issue
3. Claude re-stages the files
4. Claude creates a **new** commit (never `--amend`, which would modify the previous commit)

---

## Best Practices

1. **Let Claude read the diff first** — Always let Claude run `git diff` before committing so the message is accurate
2. **Use worktrees for parallel tasks** — Keep your main directory clean while Claude works
3. **Review PR descriptions** — Claude generates good descriptions, but always review before merging
4. **Use `--from-pr` for review feedback** — It is faster than explaining the context manually
5. **Trust the safety rails** — Claude's git safety rules exist to protect you; do not ask it to bypass them unless necessary

---

## Common Git Prompts

| Prompt | What Claude Does |
|--------|-----------------|
| "Commit these changes" | Reads diff, writes message, commits |
| "Create a PR" | Pushes branch, creates PR with `gh` |
| "Create a branch for this feature" | Creates and checks out a new branch |
| "Undo the last commit" | Runs `git reset --soft HEAD~1` (preserves changes) |
| "Show me what changed" | Runs `git diff` and summarizes |
| "Rebase onto main" | Runs `git rebase main` with conflict resolution |

---

[← Built-in Tools Reference](built-in-tools.md) | [Code Editing Workflows →](code-editing.md)

---

*Module 05, Lesson 3 — Claude Code Mastery — March 2026*
