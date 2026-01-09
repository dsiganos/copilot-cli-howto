# 09 - Advanced Techniques

**Time**: 45 minutes
**Level**: Advanced

## Overview

Master advanced features of GitHub Copilot CLI including session management, model optimization, custom configurations, and power user techniques.

## Session Management

### Understanding Sessions

A session maintains:
- Conversation history
- File context
- Decisions made
- Model state

### Resuming Sessions

```bash
# Resume the most recent session
copilot --resume

# Or use --continue
copilot --continue
```

### Session Benefits

When you resume:

```bash
$ copilot --resume

Resuming previous session...

> Remember the auth bug we were fixing?

Yes, we were working on the race condition in @src/auth/login.js.
We identified the issue but hadn't implemented the fix yet.

> Let's continue with that fix
```

### Session Persistence

Sessions are stored locally and persist across:
- Terminal closures
- System restarts
- Multiple projects (separate sessions per directory)

### Managing Sessions

```bash
# View session info
> /usage

Session Statistics:
- Started: 2 hours ago
- Messages: 45
- Files modified: 8
```

## Model Selection Strategies

### Available Models

| Model | Strengths | Best For |
|-------|-----------|----------|
| Claude Sonnet 4.5 | Best reasoning | Complex tasks |
| Claude Sonnet 4 | Fast, capable | Most tasks |
| GPT-5 | Alternative perspective | Comparison |

### Switching Models

```bash
> /model

# Or directly
> /model claude-sonnet-4
```

### When to Switch Models

```bash
# Complex reasoning task
> /model claude-sonnet-4.5
> Help me design the architecture for...

# Quick task
> /model claude-sonnet-4
> Add a simple validation check to...
```

### Comparing Models

```bash
# Get answer from default model
> How would you implement caching here?

# Switch and compare
> /model gpt-5
> Same question - how would you implement caching here?

# Compare approaches
```

## Usage Optimization

### Monitoring Usage

```bash
> /usage

Session Statistics:
- Tokens used: 45,230
- Premium requests: 8
- Estimated cost: ~$0.15
```

### Reducing Token Usage

#### 1. Be Concise

```bash
# ❌ Verbose
> Can you please look at the file called src/auth/login.js and tell me what you think about it and if there are any problems with the code and how we might fix them?

# ✅ Concise
> @src/auth/login.js review for issues
```

#### 2. Reference Instead of Paste

```bash
# ❌ Pasting large code blocks
> Here's my code: [500 lines]

# ✅ Reference the file
> @src/large-file.js analyze the main function
```

#### 3. Focus the Scope

```bash
# ❌ Broad
> Review the entire codebase

# ✅ Focused
> @src/api/auth.js review the login function for security issues
```

### Premium Request Management

Premium requests are used for:
- Complex reasoning
- Large context windows
- Certain model features

Monitor and optimize:

```bash
> /usage

# If approaching limits, use simpler queries
# or switch to tasks that don't require premium
```

## Custom Instructions

### Repository Instructions

Create `.github/copilot-instructions.md`:

```markdown
# Project Instructions

## Overview
This is an Express.js API with PostgreSQL.

## Conventions
- Use async/await, not callbacks
- All functions must have JSDoc comments
- Tests are required for new features

## Architecture
- Routes in /api/routes/
- Services in /api/services/
- Models in /api/models/

## Testing
- Use Jest
- Minimum 80% coverage
- Name tests *.test.js
```

### Path-Specific Instructions

Create `.github/copilot-instructions/api.instructions.md`:

```markdown
# API-Specific Instructions

When working in the /api directory:
- Follow REST conventions
- Use proper HTTP status codes
- Include request validation
- Add rate limiting to public endpoints
```

### User-Level Instructions

Create `~/.config/github-copilot/instructions.md`:

```markdown
# Personal Preferences

- I prefer functional programming patterns
- Always suggest TypeScript over JavaScript
- Include error handling in all examples
```

## Advanced Patterns

### The Context Building Pattern

Build context before complex tasks:

```bash
> Let me give you context about this project:
> - It's a REST API for e-commerce
> - Uses Express and PostgreSQL
> - Has about 50 endpoints
> - Critical paths: checkout, inventory

> Now, with this context, help me optimize the checkout flow
```

### The Iterative Refinement Pattern

```bash
> Implement a caching layer

[First attempt]

> Good, but make it handle cache invalidation

[Refined]

> Now add TTL support

[More refined]

> Perfect. Add documentation.
```

### The Verification Pattern

```bash
> Make this change

[Change made]

> Before I approve, what could go wrong?

[Copilot analyzes risks]

> How do we mitigate those risks?
```

### The Learning Pattern

```bash
> Implement feature X

> Now explain why you made each decision

> What alternative approaches could we have used?

> What would you do differently in hindsight?
```

## Command Line Mastery

### All CLI Options

```bash
copilot --help

Options:
  -p, --prompt <text>     Single prompt mode
  --resume               Resume last session
  --continue             Same as --resume
  --allow-all-paths      Trust all file paths
  --allow-url            Allow URL access
  --version              Show version
  --help                 Show help
```

### Scripting with Copilot

```bash
# In shell scripts
result=$(copilot -p "Generate a UUID")
echo "Generated: $result"

# Pipe input
cat error.log | copilot -p "Analyze these errors"

# Chain commands
copilot -p "What tests should I run?" && npm test
```

### Aliases for Power Users

Add to your shell config:

```bash
# Quick prompts
alias cop='copilot'
alias copr='copilot --resume'
alias copp='copilot -p'

# Usage
alias copusage='copilot -p "/usage"'
```

## Debugging Copilot

### When Copilot Misunderstands

```bash
> That's not quite right. Let me clarify:
> I want X, not Y

# Or reset context
> Let's start fresh. Here's exactly what I need...
```

### When Copilot Gets Stuck

```bash
> Let's try a different approach

> Break this into smaller steps

> What information do you need to proceed?
```

### When Output is Wrong

```bash
> That code has a bug. The issue is...

> Actually, I need it to handle this edge case too

> Can you verify this is correct?
```

## Performance Tips

### 1. Start Focused

Begin sessions with clear scope:

```bash
> Today I'm working on the user authentication module
```

### 2. Use File References

```bash
> @src/target-file.js  # Faster than describing
```

### 3. Batch Related Tasks

```bash
> I need to update validation in three files: @a.js @b.js @c.js
> Make the same change to all of them
```

### 4. Leverage Session Context

```bash
# First session establishes context
> @src/api/ explain the architecture

# Resume later
copilot --resume
> Add a new endpoint following the pattern we discussed
```

## Integration Patterns

### With Git Workflows

```bash
# Pre-commit review
> Review my staged changes for issues
> !git diff --cached

# Post-merge verification
> !git pull
> What changed and does anything need attention?
```

### With CI/CD

```bash
# Analyze CI failures
> The CI failed. Here's the log: [paste]
> What's wrong and how do I fix it?

# Generate CI configs
> Create a GitHub Actions workflow for this project
```

### With IDEs

Use Copilot CLI alongside your IDE:
- IDE for editing
- CLI for complex discussions
- CLI for git operations
- CLI for architecture decisions

## Quick Reference

| Feature | Command/Usage |
|---------|---------------|
| Resume session | `copilot --resume` |
| Single prompt | `copilot -p "text"` |
| Change model | `/model` |
| Check usage | `/usage` |
| Trust all paths | `--allow-all-paths` |
| Custom instructions | `.github/copilot-instructions.md` |

## Next Steps

Now that you've mastered advanced features:

1. [10-best-practices](../10-best-practices/) - Security and best practices
2. Apply these techniques to your daily work
3. Create custom agents for your workflow

---

**Estimated completion time**: 45 minutes
**Previous**: [08-workflows](../08-workflows/)
**Next**: [10-best-practices](../10-best-practices/)
