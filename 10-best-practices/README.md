# 10 - Best Practices and Security

**Time**: 30 minutes
**Level**: All Levels

## Overview

Essential best practices, security considerations, and guidelines for safe and effective use of GitHub Copilot CLI.

## Security Best Practices

### 1. Review Before Approving

**ALWAYS review changes before approving:**

```bash
> @src/config.js update the database connection

Proposed changes:
- connectionString: 'localhost:5432'
+ connectionString: 'production.db:5432'

Apply changes? (y/n)
```

**Take time to verify the change is correct and safe.**

### 2. Be Careful with Destructive Operations

```bash
# ⚠️ These require extra caution:
> Delete unused files
> Clean up the codebase
> Reset the database
> Remove user data
```

Always ask:
- What exactly will be deleted?
- Is there a backup?
- Can this be undone?

### 3. Protect Sensitive Data

**DON'T include in prompts:**
- Passwords or API keys
- Personal information
- Proprietary business logic
- Security vulnerabilities (unless fixing)

```bash
# ❌ Bad
> Connect to database with password "secret123"

# ✅ Good
> Connect to database using environment variable
```

### 4. Verify External Commands

Before running suggested commands:

```bash
> How do I deploy?

Copilot suggests: ./deploy.sh --force

# Before running, understand what --force does!
> What does the --force flag do?
```

### 5. Trust Directories Carefully

Only trust directories you're actively working with:

```bash
# Be selective
> /add-dir ~/my-project

# Avoid
copilot --allow-all-paths  # Only when necessary
```

## Permission Management

### Understanding Permissions

| Action | Permission Level |
|--------|-----------------|
| Read file contents | Trusted directory |
| Edit existing file | Approval required |
| Create new file | Approval required |
| Delete file | Explicit approval |
| Run commands | Explicit approval |

### Safe Approval Patterns

```bash
# Review each change individually
Apply changes? (y/n) y  # After reviewing

# Or approve batch with caution
Apply all changes? (y/n/review) review  # Check first
```

### When to Say No

Say **n** (no) when:
- You don't understand the change
- The change seems too broad
- It modifies files you didn't expect
- It includes hardcoded secrets
- Something feels wrong

## Code Quality

### 1. Verify Correctness

```bash
# After AI makes changes
> Does this code handle all edge cases?
> What could go wrong with this implementation?
> Are there any security issues?
```

### 2. Test Changes

```bash
# Always test after modifications
> !npm test

# If tests fail
> Fix the failing tests
```

### 3. Review Generated Code

Don't blindly accept generated code:

```bash
> Generate a login function

[Code generated]

# Review for:
# - SQL injection
# - Password handling
# - Error messages (no info leakage)
# - Rate limiting
```

### 4. Maintain Code Style

```bash
# Ask for style consistency
> Follow the existing code style in this project

# Or specify
> Use async/await and follow our ESLint rules
```

## Privacy Considerations

### What Copilot Sees

- Your prompts
- Files you reference with @
- Command outputs you share
- Session history

### What to Avoid Sharing

- Credentials and secrets
- Personal data (PII)
- Proprietary algorithms
- Compliance-sensitive data

### Best Practices

```bash
# Use environment variables
> @.env.example show me the structure
# Not @.env with real values

# Sanitize sensitive data
> Here's the error log (sanitized): [redacted passwords]
```

## Team Guidelines

### Consistent Usage

Establish team conventions:

```markdown
# Team Copilot Guidelines

1. Always review before approving
2. Test changes before committing
3. Don't share credentials via Copilot
4. Use repository instructions for consistency
5. Document AI-assisted changes in commits
```

### Repository Instructions

Create `.github/copilot-instructions.md`:

```markdown
# Project Standards

## Security
- Never hardcode credentials
- Use parameterized queries
- Validate all input

## Code Style
- Follow existing patterns
- Add tests for new code
- Include error handling
```

### Knowledge Sharing

```bash
# Document useful patterns
> This prompt worked well, save it to our team wiki

# Share custom agents
.github/copilot/agents/team-agent.yml
```

## Error Handling

### When Copilot Makes Mistakes

```bash
> That's incorrect. The issue is [explanation]

> Undo the last change

> Let's try a different approach
```

### When Things Go Wrong

```bash
# Undo file changes
> !git checkout -- src/file.js

# Revert all changes
> !git reset --hard HEAD

# Check what changed
> !git diff
```

## Cost Management

### Monitor Usage

```bash
> /usage

# Check regularly during intensive sessions
```

### Optimize Prompts

```bash
# ❌ Wasteful
> Tell me everything about this codebase

# ✅ Efficient
> @src/api/auth.js explain the login function
```

### Use Appropriate Models

```bash
# Complex reasoning
> /model claude-sonnet-4.5

# Simple tasks
> /model claude-sonnet-4
```

## Compliance

### Audit Trail

For regulated environments:

```bash
# Document AI assistance in commits
git commit -m "feat: add validation

Co-authored-by: GitHub Copilot"
```

### Data Handling

- Know your organization's AI policy
- Understand data retention
- Be aware of compliance requirements

## Checklist

### Before Each Session

- [ ] Am I in the right directory?
- [ ] Do I trust this directory?
- [ ] Is there sensitive data I should avoid?

### Before Approving Changes

- [ ] Do I understand what's changing?
- [ ] Have I reviewed the diff?
- [ ] Is this what I asked for?
- [ ] Are there any security concerns?

### After Making Changes

- [ ] Do the tests pass?
- [ ] Does the code work as expected?
- [ ] Is the code style consistent?
- [ ] Should I commit this now?

### Before Committing

- [ ] Review all changes with `git diff`
- [ ] Are there any secrets in the diff?
- [ ] Is the commit message accurate?
- [ ] Should I attribute AI assistance?

## Common Mistakes to Avoid

### 1. Blind Approval

```bash
# ❌ Don't just spam 'y'
Apply changes? y y y y

# ✅ Review each change
Apply changes? [read the diff first] y
```

### 2. Over-Trusting

```bash
# ❌ Trust everything
copilot --allow-all-paths

# ✅ Trust specifically
> /add-dir ~/specific-project
```

### 3. Sharing Secrets

```bash
# ❌ Including credentials
> Fix the connection to postgres://user:password@host

# ✅ Using variables
> Fix the database connection using DATABASE_URL env var
```

### 4. Skipping Tests

```bash
# ❌ Assuming it works
> Make the change
> !git commit

# ✅ Verifying
> Make the change
> !npm test
> !git commit
```

## Summary

### Key Principles

1. **Review everything** - Never blindly approve
2. **Test changes** - Verify before committing
3. **Protect secrets** - Never share credentials
4. **Stay in control** - You make the final decisions
5. **Learn continuously** - Understand what Copilot does

### Remember

GitHub Copilot CLI is a powerful tool, but **you are responsible** for:
- Code quality
- Security
- Correctness
- Compliance

Use it wisely, and it will significantly boost your productivity while maintaining high standards.

---

**Estimated completion time**: 30 minutes
**Previous**: [09-advanced](../09-advanced/)

---

**Congratulations!** You've completed the GitHub Copilot CLI learning guide.

**Return to**: [Main README](../README.md)
