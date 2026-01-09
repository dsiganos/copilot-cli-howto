# Claude Code vs GitHub Copilot CLI

A comprehensive comparison between Claude Code and GitHub Copilot CLI - two agentic AI assistants for the command line.

## Overview

Both Claude Code and GitHub Copilot CLI are **agentic AI assistants** that run in your terminal. They are very similar in capabilities, both able to:

- Edit files directly
- Run shell commands
- Maintain conversation context
- Use MCP (Model Context Protocol)
- Support custom instructions

| Feature | GitHub Copilot CLI | Claude Code |
|---------|-------------------|-------------|
| **Type** | Agentic assistant | Agentic assistant |
| **Primary model** | Claude Sonnet 4.5 | Claude Sonnet |
| **File editing** | ✅ Yes | ✅ Yes |
| **Command execution** | ✅ Yes | ✅ Yes |
| **Session persistence** | ✅ Yes | ✅ Yes |
| **MCP support** | ✅ Yes | ✅ Yes |
| **Custom instructions** | ✅ Yes | ✅ Yes |

## Key Differences

### 1. GitHub Integration

**Copilot CLI** has deep GitHub integration:

```bash
> Show me open issues
> Create a PR for these changes
> /delegate  # Hand off to GitHub's cloud agent
```

**Claude Code** works with any Git provider but doesn't have native GitHub features.

### 2. Delegation Feature

**Copilot CLI** can delegate tasks to GitHub's cloud agent:

```bash
> /delegate
```

This hands off complex tasks to run asynchronously in the cloud.

**Claude Code** runs entirely locally - no cloud delegation.

### 3. Custom Instructions Location

| Tool | Main File | Location |
|------|-----------|----------|
| Claude Code | `CLAUDE.md` | Project root |
| Copilot CLI | `copilot-instructions.md` | `.github/` directory |

### 4. Starting Commands

| Tool | Command |
|------|---------|
| Claude Code | `claude` |
| Copilot CLI | `copilot` |

### 5. File Reference Syntax

| Tool | Syntax |
|------|--------|
| Claude Code | Direct file paths |
| Copilot CLI | `@filepath` |

### 6. Shell Passthrough

| Tool | Syntax |
|------|--------|
| Claude Code | Bash tool |
| Copilot CLI | `!command` |

### 7. Pricing Model

| Tool | Pricing |
|------|---------|
| Claude Code | Claude API (pay-per-use or subscription) |
| Copilot CLI | GitHub Copilot subscription ($10-19/month) |

## Feature Comparison

### Core Features

| Feature | Claude Code | Copilot CLI |
|---------|-------------|-------------|
| Interactive mode | ✅ | ✅ |
| Single prompt mode | ✅ `-p` | ✅ `-p` |
| Resume sessions | ✅ `--continue` | ✅ `--resume` |
| File reading | ✅ | ✅ `@file` |
| File editing | ✅ | ✅ |
| File creation | ✅ | ✅ |
| Command execution | ✅ | ✅ `!cmd` |
| Permission system | ✅ | ✅ |

### Extensions

| Feature | Claude Code | Copilot CLI |
|---------|-------------|-------------|
| MCP servers | ✅ | ✅ `/mcp add` |
| Custom agents | ✅ | ✅ `/agent` |
| Custom instructions | ✅ CLAUDE.md | ✅ copilot-instructions.md |
| Hooks | ✅ | ❓ |
| Skills | ✅ | ❓ |

### Platform Integration

| Feature | Claude Code | Copilot CLI |
|---------|-------------|-------------|
| GitHub Issues | ❌ | ✅ |
| GitHub PRs | ❌ | ✅ |
| GitHub Actions | ❌ | ✅ |
| Cloud delegation | ❌ | ✅ `/delegate` |
| IDE integration | ✅ VSCode, JetBrains | ❌ |

### Models

| Tool | Available Models |
|------|------------------|
| Claude Code | Claude models only |
| Copilot CLI | Claude Sonnet 4.5 (default), Claude Sonnet 4, GPT-5 |

## Workflow Comparison

### Starting a Session

**Claude Code:**
```bash
claude
```

**Copilot CLI:**
```bash
copilot
```

### Referencing Files

**Claude Code:**
```bash
> Read src/config.js
> Edit src/config.js to change the port
```

**Copilot CLI:**
```bash
> @src/config.js show me this file
> @src/config.js change the port
```

### Running Commands

**Claude Code:**
```bash
> Run npm test
[Uses Bash tool]
```

**Copilot CLI:**
```bash
> !npm test
[Runs directly]
```

### Custom Instructions

**Claude Code** - `CLAUDE.md` in project root:
```markdown
# Project Context
This is a Node.js API...
```

**Copilot CLI** - `.github/copilot-instructions.md`:
```markdown
# Project Context
This is a Node.js API...
```

## When to Use Which

### Use GitHub Copilot CLI When:

- ✅ You need GitHub integration (issues, PRs)
- ✅ You want to delegate tasks to cloud agents
- ✅ You have a Copilot subscription
- ✅ You work primarily with GitHub repositories
- ✅ You want access to multiple models

### Use Claude Code When:

- ✅ You work with non-GitHub repositories
- ✅ You need IDE integration (VSCode, JetBrains)
- ✅ You prefer pay-per-use pricing
- ✅ You want Claude-specific features
- ✅ You need hooks and skills

### Either Tool Works Well For:

- General coding assistance
- File editing and refactoring
- Code explanation
- Debugging
- Test generation
- Documentation

## Migration Guide

### From Claude Code to Copilot CLI

1. **Custom instructions**: Move `CLAUDE.md` to `.github/copilot-instructions.md`
2. **File references**: Change `Read file.js` to `@file.js`
3. **Shell commands**: Use `!command` instead of asking to run
4. **MCP servers**: Re-register with `/mcp add`

### From Copilot CLI to Claude Code

1. **Custom instructions**: Move `.github/copilot-instructions.md` to `CLAUDE.md`
2. **File references**: Use direct paths instead of `@`
3. **Shell commands**: Ask to run commands normally
4. **GitHub features**: Use `gh` CLI manually for GitHub operations

## Using Both Together

You can use both tools depending on the task:

```bash
# Use Claude Code for general development
claude
> Help me refactor this module

# Use Copilot CLI for GitHub tasks
copilot
> Create a PR for my changes
> What issues are assigned to me?
```

## Summary

Both tools are excellent agentic AI assistants. The main factors for choosing:

| If You Need | Choose |
|-------------|--------|
| GitHub integration | Copilot CLI |
| Cloud delegation | Copilot CLI |
| IDE integration | Claude Code |
| Non-GitHub repos | Claude Code |
| Multiple AI models | Copilot CLI |
| Pay-per-use pricing | Claude Code |

For many developers, having both installed and using each for its strengths is the optimal approach.

---

**Related:**
- [GitHub Copilot CLI Repository](https://github.com/github/copilot-cli)
- [Claude Code Documentation](https://docs.anthropic.com/claude-code)
- [Main README](./README.md)
