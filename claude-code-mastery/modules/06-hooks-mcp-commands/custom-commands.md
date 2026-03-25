# Custom Slash Commands

**Module 06, Lesson 3 --- Claude Code Mastery**

**Instructor: Jabbir Basha, Principal AI Engineer**

---

## What Are Custom Commands?

Custom slash commands are reusable prompt templates that you invoke from within Claude Code using the `/` prefix. They let you encode multi-step workflows, review checklists, deployment procedures, and any other repeated task as a single command that your entire team can share through git.

When you type `/` in Claude Code, you see both built-in commands and any custom commands discovered in your project or user directory.

---

## File Structure

Custom commands are Markdown files stored in the `.claude/commands/` directory:

```
your-project/
  .claude/
    commands/
      review-pr.md        -->  /project:review-pr
      deploy.md            -->  /project:deploy
      test-feature.md      -->  /project:test-feature
      onboarding/
        setup.md           -->  /project:onboarding:setup
```

| Location | Command Prefix | Shared via Git? |
|----------|---------------|-----------------|
| `.claude/commands/` (project) | `/project:command-name` | Yes |
| `~/.claude/commands/` (user) | `/user:command-name` | No |

Subdirectories create nested namespaces separated by colons.

---

## Anatomy of a Command File

A command file is plain Markdown. Its contents become the prompt sent to Claude when the command is invoked. The filename (without `.md`) becomes the command name.

**Example: `.claude/commands/review-pr.md`**

```markdown
Review the following pull request or code changes carefully.

Focus on:
1. Logic errors and potential bugs
2. Security vulnerabilities (injection, auth bypass, data exposure)
3. Performance issues (N+1 queries, unnecessary allocations)
4. Code style and consistency with the existing codebase
5. Test coverage gaps

For each issue found, provide:
- **File and line**: exact location
- **Severity**: critical / warning / suggestion
- **Description**: what is wrong and why
- **Fix**: concrete code suggestion

Summarize your findings in a table at the end.

$ARGUMENTS
```

---

## The $ARGUMENTS Placeholder

The `$ARGUMENTS` placeholder is replaced with whatever text the user types after the command name:

```
> /project:review-pr src/auth/login.ts
```

In the example above, `$ARGUMENTS` is replaced with `src/auth/login.ts`. This lets you parameterize your commands.

| Input | `$ARGUMENTS` Value |
|-------|-------------------|
| `/project:deploy staging` | `staging` |
| `/project:test-feature user authentication` | `user authentication` |
| `/project:review-pr --diff HEAD~3` | `--diff HEAD~3` |
| `/project:deploy` (no argument) | *(empty string)* |

---

## Example Commands

### 1. Code Review Command

**`.claude/commands/review-pr.md`**

```markdown
You are an expert code reviewer. Review the code changes described below.

Check for:
- Correctness and edge cases
- Security vulnerabilities
- Performance concerns
- Adherence to project coding standards
- Missing or inadequate tests

Present findings as a Markdown table with columns: File, Line, Severity, Issue, Suggested Fix.

If no issues are found, confirm the code looks good and note any positive patterns.

$ARGUMENTS
```

**Usage:** `/project:review-pr the changes in the last commit`

### 2. Deployment Workflow Command

**`.claude/commands/deploy.md`**

```markdown
Execute a deployment workflow for the target environment specified below.

Steps:
1. Run the full test suite and report results
2. Check for any uncommitted changes and warn if present
3. Verify the current branch matches the expected deployment branch
4. Build the project for production
5. Show a summary of what will be deployed (changed files since last tag)
6. Ask for final confirmation before proceeding

Target environment: $ARGUMENTS

If no environment is specified, default to "staging" and confirm with me.
```

**Usage:** `/project:deploy production`

### 3. Feature Testing Command

**`.claude/commands/test-feature.md`**

```markdown
Test the following feature thoroughly:

1. Identify all files related to the feature described below
2. Check existing test coverage for those files
3. Run existing tests and report results
4. Suggest additional test cases for edge cases and error paths
5. Write the missing tests and run them
6. Provide a coverage summary

Feature to test: $ARGUMENTS
```

**Usage:** `/project:test-feature user authentication flow`

### 4. Bug Investigation Command

**`.claude/commands/investigate-bug.md`**

```markdown
Investigate the following bug report:

$ARGUMENTS

Approach:
1. Search the codebase for relevant files and functions
2. Identify the likely root cause
3. Check git blame to understand when the issue was introduced
4. Propose a fix with minimal scope
5. Suggest a test that would catch this regression
```

**Usage:** `/project:investigate-bug Users receive 500 error when submitting empty forms`

### 5. Documentation Generator

**`.claude/commands/document.md`**

```markdown
Generate or update documentation for the following:

$ARGUMENTS

Requirements:
- Add JSDoc/docstring comments to all public functions
- Update or create a README section if appropriate
- Include usage examples
- Note any configuration options or environment variables
```

**Usage:** `/project:document the API routes in src/api/`

---

## Sharing Commands via Git

Because project commands live in `.claude/commands/`, they are committed alongside your code:

```bash
git add .claude/commands/
git commit -m "Add team code review and deploy commands"
git push
```

Every team member who pulls the repository automatically gets the same set of commands. This ensures:

| Benefit | Description |
|---------|-------------|
| Consistency | Everyone follows the same review checklist |
| Discoverability | New team members find workflows by typing `/` |
| Version control | Command changes are tracked in git history |
| Code review | Command templates can be reviewed in PRs |

---

## Personal vs Project Commands

| Aspect | Project Commands | User Commands |
|--------|-----------------|---------------|
| Path | `.claude/commands/` | `~/.claude/commands/` |
| Prefix | `/project:` | `/user:` |
| Shared | Yes (via git) | No (local only) |
| Best for | Team workflows, project standards | Personal shortcuts, cross-project utilities |

Personal commands are ideal for things that do not belong in a shared repository --- for example, a command that references your personal note-taking system or a specific formatting style you prefer.

---

## Best Practices

1. **Be specific in prompts** --- vague commands produce vague results. Include concrete criteria and output formats.
2. **Always include `$ARGUMENTS`** --- even if optional, it gives users the flexibility to add context.
3. **Use numbered steps** --- Claude follows ordered instructions more reliably than unstructured prose.
4. **Request structured output** --- ask for tables, bullet lists, or specific sections so results are consistent.
5. **Test your commands** --- run them several times with different arguments to verify they produce useful output.
6. **Keep commands focused** --- one command should do one workflow. Compose multiple commands rather than building a single mega-command.

---

## Navigation

| Direction | Link |
|-----------|------|
| Previous | [MCP Servers](mcp-servers.md) |
| Next | [Skills System](skills-system.md) |
| Module Home | [Module 06 Overview](README.md) |
