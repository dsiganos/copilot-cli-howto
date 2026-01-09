# 07 - GitHub Integration

**Time**: 30 minutes
**Level**: Intermediate

## Overview

Learn how GitHub Copilot CLI integrates with GitHub's ecosystem - working with issues, pull requests, repositories, and the `/delegate` feature.

## GitHub Integration Features

Copilot CLI has deep integration with GitHub:

- Access repository information
- Work with issues and PRs
- Delegate tasks to cloud agents
- Query GitHub data naturally

## Working with Repositories

### Repository Information

```bash
> What are the recent commits in this repo?

> Show me the branch structure

> What's the most active file in this repository?

> Who are the main contributors?
```

### Repository Context

Copilot automatically understands your GitHub repository:

```bash
> What open issues do we have?

> Are there any stale pull requests?

> Show me the CI/CD workflow status
```

## Working with Issues

### Viewing Issues

```bash
> List open issues in this repository

> Show me issues labeled as 'bug'

> What are the high-priority issues?

> Find issues assigned to me
```

### Creating Issues

```bash
> Create an issue for the bug we just found in the auth module

> Create a feature request issue for adding dark mode

> Create an issue tracking the refactoring work we discussed
```

### Analyzing Issues

```bash
> Summarize issue #42

> What's the discussion history on issue #123?

> Are there any duplicate issues to #15?
```

## Working with Pull Requests

### Viewing PRs

```bash
> Show open pull requests

> List PRs waiting for review

> What PRs have conflicts?

> Show my open PRs
```

### Analyzing PRs

```bash
> Summarize the changes in PR #87

> What tests are failing in PR #92?

> Review the code changes in PR #55
```

### Creating PRs

After making changes:

```bash
> Create a pull request for these changes

> Create a PR with a detailed description of the auth refactoring
```

## The /delegate Command

### What is /delegate?

Hand off complex or long-running tasks to GitHub's cloud-based Copilot coding agent:

```bash
> /delegate
```

### When to Use /delegate

- Large refactoring tasks
- Multi-file changes
- Tasks that take many iterations
- When you need to step away

### Delegation Workflow

```bash
# Describe the task
> Refactor the authentication system to use OAuth2 instead of sessions

# Review the plan
[Copilot shows the proposed plan]

> This looks good

# Delegate
> /delegate

Task delegated to Copilot coding agent.
Track progress: https://github.com/user/repo/copilot/task/456
```

### Tracking Delegated Tasks

Once delegated:
- Task runs asynchronously in the cloud
- You receive GitHub notifications on progress
- Results appear as PRs or commits
- You can continue working locally

```bash
> What's the status of my delegated task?

> Show me the PR created by the delegated task
```

## Natural Language GitHub Queries

### Issues

```bash
> How many bugs were filed this month?

> What issues have been open the longest?

> Show me issues that mention "performance"
```

### Pull Requests

```bash
> What's our average time to merge PRs?

> Which PRs have been approved but not merged?

> Show PRs that modify the API
```

### Repository Stats

```bash
> How active has this repo been lately?

> What files change most frequently?

> Show contribution stats for the team
```

## Practical Examples

### Bug Investigation Workflow

```bash
# Find related issues
> Are there issues related to login failures?

# Look at the code
> @src/auth.js show me the login function

# Check recent changes
> What commits modified auth.js recently?

# Create an issue
> Create an issue documenting this bug
```

### PR Review Workflow

```bash
# List PRs to review
> Show PRs waiting for my review

# Review a specific PR
> Summarize the changes in PR #123

# Check for issues
> Are there any concerns with the code in PR #123?

# Leave feedback
> What feedback should I give on this PR?
```

### Feature Development Workflow

```bash
# Check if issue exists
> Is there an issue for adding dark mode?

# Start implementation
> Let's implement the dark mode feature

[Work on implementation]

# Create PR
> Create a PR for these changes, referencing issue #45
```

### Delegating Large Tasks

```bash
# Describe a big task
> We need to migrate from JavaScript to TypeScript

# Get a plan
> What would this migration involve?

[Copilot outlines the plan]

# Delegate
> /delegate

# Continue with other work while cloud agent processes
```

## GitHub Actions Integration

### Viewing Workflows

```bash
> What GitHub Actions workflows do we have?

> Show me the status of the CI workflow

> Why did the last workflow run fail?
```

### Understanding Failures

```bash
> The deploy workflow failed, what went wrong?

> Show me the logs from the failed test job

> How do I fix this workflow error?
```

## Best Practices

### 1. Use Specific References

```bash
# ✅ Specific
> Show me issue #42

# ❌ Vague
> Show me that issue
```

### 2. Provide Context for Delegation

```bash
# ✅ Clear task
> /delegate
Migrate the authentication module to use JWT tokens.
Keep backward compatibility with existing sessions.
Add tests for the new functionality.

# ❌ Vague
> /delegate
Fix auth
```

### 3. Review Before Creating

Before creating issues or PRs:

```bash
> Show me a preview of the issue/PR you'll create

[Review]

> Looks good, create it
```

### 4. Link Related Items

```bash
> Create a PR that closes issue #42

> Create an issue that references PR #55
```

## Troubleshooting

### "Not authenticated"

```bash
> /login
```

### "Repository not found"

Ensure you're in a directory with a Git repository:

```bash
> !git remote -v
```

### "No permissions"

Check your GitHub token has required scopes:
- `repo` for private repositories
- `issues` for issue access
- `pull_request` for PR access

### Delegated task not progressing

```bash
> What's the status of delegated task #456?

# Check GitHub directly
> !gh copilot task status 456
```

## Quick Reference

| Action | Command/Query |
|--------|---------------|
| View issues | "Show open issues" |
| View PRs | "Show open pull requests" |
| Create issue | "Create an issue for..." |
| Create PR | "Create a pull request..." |
| Delegate task | `/delegate` |
| Check task status | "Status of delegated task" |
| View workflows | "Show CI workflow status" |

## Next Steps

Now that you understand GitHub integration:

1. [08-workflows](../08-workflows/) - Real-world workflows
2. [09-advanced](../09-advanced/) - Advanced techniques
3. [10-best-practices](../10-best-practices/) - Best practices

---

**Estimated completion time**: 30 minutes
**Previous**: [06-mcp-extensions](../06-mcp-extensions/)
**Next**: [08-workflows](../08-workflows/)
