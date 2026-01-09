# 05 - Shell Integration

**Time**: 20 minutes
**Level**: Intermediate

## Overview

Learn how to execute shell commands directly from GitHub Copilot CLI using the `!` prefix, combining AI assistance with direct command execution.

## The ! Syntax

Prefix any command with `!` to run it directly in your shell:

```bash
> !ls -la
> !git status
> !npm test
```

This bypasses the AI and executes the command immediately.

## Basic Usage

### Running Commands

```bash
# List files
> !ls

# Check git status
> !git status

# View current directory
> !pwd

# Run tests
> !npm test
```

### Command Output

The output is displayed directly:

```bash
> !git status
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```

## When to Use !

### Direct Execution (!)

Use `!` when you know exactly what command to run:

```bash
> !docker ps
> !kubectl get pods
> !npm install lodash
```

### AI Assistance (no !)

Ask without `!` when you want Copilot to help:

```bash
> How do I list running docker containers?

Copilot: You can use: docker ps
Would you like me to run this command?
```

## Common Patterns

### Check Then Act

```bash
# Check status first
> !git status

# Ask AI about what you see
> What do these changes look like?

# Then act
> !git add .
```

### Verify AI Changes

```bash
# AI makes changes
> @src/config.js update the API URL

# Verify with shell command
> !git diff src/config.js

# Commit if good
> !git add src/config.js && git commit -m "Update API URL"
```

### Explore Then Modify

```bash
# Explore
> !find . -name "*.test.js"

# Ask AI
> Can you tell me which of these tests are failing?

# Fix
> Fix the failing tests
```

## Combining AI and Shell

### Pattern 1: AI Suggests, You Execute

```bash
> How do I find large files in this directory?

Copilot: You can use this command:
find . -type f -size +10M

> !find . -type f -size +10M
```

### Pattern 2: Shell Output to AI

```bash
> !cat error.log | tail -20

[Error output displayed]

> What's causing these errors?
```

### Pattern 3: Iterative Development

```bash
> !npm test

[Tests fail]

> Fix the failing test in @src/utils.test.js

[AI fixes the test]

> !npm test

[Tests pass]
```

## Practical Examples

### Git Workflow

```bash
# Check status
> !git status

# See changes
> !git diff

# Ask AI about changes
> Are these changes safe to commit?

# Stage and commit
> !git add .
> !git commit -m "feat: add user validation"
```

### Docker Workflow

```bash
# List containers
> !docker ps

# Check logs
> !docker logs container-name --tail 50

# Ask AI
> What's wrong with this container based on the logs?
```

### Node.js Workflow

```bash
# Install dependencies
> !npm install

# Run tests
> !npm test

# If tests fail
> Help me fix the failing tests

# Run again
> !npm test
```

### Build Workflow

```bash
# Build project
> !npm run build

# If errors
> Explain these build errors

# Fix
> Fix the type error in @src/api.ts

# Build again
> !npm run build
```

## Advanced Usage

### Piping Commands

```bash
> !cat package.json | grep dependencies
> !ls -la | grep ".js"
> !git log --oneline | head -10
```

### Environment Variables

```bash
> !echo $PATH
> !env | grep NODE
> !export DEBUG=true && npm test
```

### Chaining Commands

```bash
> !npm test && npm run build
> !git add . && git commit -m "update" && git push
```

### Background Processes

```bash
> !npm run dev &
> !docker-compose up -d
```

## Safety Considerations

### Commands That Require Caution

```bash
# Destructive commands - be careful!
> !rm -rf ...     # Delete files
> !git reset --hard  # Lose changes
> !docker system prune  # Remove containers
```

### Best Practices

1. **Preview before executing destructive commands**
   ```bash
   > What would `rm -rf node_modules` do?
   > !rm -rf node_modules  # Only after understanding
   ```

2. **Use dry-run when available**
   ```bash
   > !rsync -avz --dry-run source/ dest/
   ```

3. **Check git status frequently**
   ```bash
   > !git status
   > !git diff
   ```

## Combining with File Operations

### Edit Then Run

```bash
# Edit file
> @package.json add a "lint" script

# Run the new script
> !npm run lint
```

### Run Then Edit

```bash
# Run tests
> !npm test

# Fix based on output
> @src/user.test.js fix the failing assertion
```

### Generate Then Execute

```bash
# Generate script
> Create @scripts/deploy.sh for deploying to production

# Make executable
> !chmod +x scripts/deploy.sh

# Run it
> !./scripts/deploy.sh
```

## Shell vs AI Decision Guide

| Situation | Use | Why |
|-----------|-----|-----|
| Know exact command | `!command` | Faster, direct |
| Need help with command | Ask AI | Get guidance |
| Checking output | `!command` | See raw output |
| Analyzing output | AI | Get interpretation |
| Destructive actions | Ask AI first | Safety check |
| Repetitive tasks | `!command` | Efficiency |
| Complex pipelines | Ask AI | Get help building |

## Troubleshooting

### Command Not Found

```bash
> !mycmd
bash: mycmd: command not found

# Check if installed
> !which mycmd
> !command -v mycmd
```

### Permission Denied

```bash
> !./script.sh
bash: permission denied

# Fix permissions
> !chmod +x ./script.sh
> !./script.sh
```

### Environment Issues

```bash
# Check environment
> !env
> !echo $PATH

# Source profile
> !source ~/.bashrc
```

## Quick Reference

| Action | Syntax |
|--------|--------|
| Run command | `!command` |
| Run with args | `!command arg1 arg2` |
| Pipe commands | `!cmd1 \| cmd2` |
| Chain commands | `!cmd1 && cmd2` |
| Background | `!command &` |
| See output and analyze | `!cmd` then ask AI |

## Next Steps

Now that you can run shell commands:

1. [06-mcp-extensions](../06-mcp-extensions/) - Extend capabilities
2. [07-github-integration](../07-github-integration/) - Work with GitHub
3. [08-workflows](../08-workflows/) - Real-world workflows

---

**Estimated completion time**: 20 minutes
**Previous**: [04-file-operations](../04-file-operations/)
**Next**: [06-mcp-extensions](../06-mcp-extensions/)
