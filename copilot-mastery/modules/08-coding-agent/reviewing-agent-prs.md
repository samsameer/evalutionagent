# Reviewing Agent Pull Requests

**Module 08, Lesson 3 | GitHub Copilot Mastery — March 2026**
**Instructor:** Jabbir Basha, Principal AI Engineer

---

## Overview

When the coding agent creates a pull request, it is your responsibility to **carefully review it** before merging. AI-generated code can be impressive, but it needs the same scrutiny as any human-authored PR — often more, because the AI may make subtle errors.

---

## Anatomy of an Agent-Created PR

Agent PRs typically include:

### 1. Summary Section
A detailed description of what was implemented and why.

### 2. Changes List
A file-by-file breakdown of modifications.

### 3. Session Log
A link to the agent's **reasoning log** — showing how it:
- Analyzed the issue
- Explored the codebase
- Made implementation decisions
- Handled errors during testing

### 4. Test Results
Whether the agent ran tests and their outcomes.

---

## Review Checklist for Agent PRs

### Code Correctness
- [ ] Does the code actually solve the issue?
- [ ] Are there any logical errors or edge cases missed?
- [ ] Does error handling cover realistic failure scenarios?
- [ ] Are return types and null checks correct?

### Security
- [ ] No hardcoded secrets, keys, or passwords
- [ ] No SQL injection or XSS vulnerabilities
- [ ] Input validation is present for user-facing code
- [ ] No overly permissive file or API access

### Code Quality
- [ ] Follows existing project patterns and conventions
- [ ] No unnecessary complexity or over-engineering
- [ ] Variable and function names are descriptive
- [ ] No dead code or unused imports

### Tests
- [ ] Tests actually test the right things
- [ ] Edge cases are covered
- [ ] Mocks are reasonable and not hiding bugs
- [ ] All tests pass (check CI)

### Dependencies
- [ ] New dependencies are necessary and well-maintained
- [ ] License compatibility is verified
- [ ] No known security vulnerabilities in new packages

---

## Requesting Changes

If the PR needs modifications, you have two options:

### Option 1: Request Changes via Review Comments

Leave review comments on specific lines. The coding agent will:
1. Read your comments
2. Make the requested changes
3. Push new commits to the PR
4. Notify you when done

### Option 2: Make Changes Yourself

Check out the branch and make changes directly:

```bash
git fetch origin
git checkout copilot/issue-123-fix-validation
# Make your changes
git commit -m "Address review feedback"
git push
```

---

## Tips for Working with Agent PRs

1. **Always run the code locally** — Do not just read the diff
2. **Check the session log** — Understand why the agent made specific decisions
3. **Test edge cases** — The agent may miss uncommon scenarios
4. **Verify CI passes** — Do not merge with failing checks
5. **Review dependencies carefully** — The agent may add unnecessary packages

---

## Navigation

| Direction | Link |
|-----------|------|
| Module Home | [Module 08: Coding Agent](README.md) |
| Previous Lesson | [Assigning Issues](assigning-issues.md) |
| Next Lesson | [Agent Configuration & Permissions](agent-configuration.md) |

---

*GitHub Copilot Mastery — A course by Jabbir Basha, Principal AI Engineer — March 2026*
