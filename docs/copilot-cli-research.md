# GitHub Copilot CLI Research

> This document contains research about the NEW GitHub Copilot CLI tool (the `copilot` command).

## Overview

GitHub Copilot CLI is an **agentic AI assistant** that brings AI-powered coding assistance directly to your terminal. It's powered by the same agentic technology as GitHub's Copilot coding agent.

**Important:** This is NOT the same as the old `gh copilot` extension (which was deprecated October 25, 2025).

## Installation

```bash
# macOS/Linux
brew install copilot-cli
# or
npm install -g @github/copilot

# Windows
winget install GitHub.Copilot

# Universal
curl -fsSL https://gh.io/copilot-install | bash
```

## Starting the Tool

```bash
# Interactive mode
copilot

# With a prompt
copilot -p "your prompt here"
copilot --prompt "your prompt here"

# Resume previous session
copilot --resume
copilot --continue
```

## Models Available

Default model is **Claude Sonnet 4.5**. Other options:
- Claude Sonnet 4
- GPT-5

Change with `/model` slash command.

## Slash Commands

| Command | Description |
|---------|-------------|
| `/login` | Authenticate to GitHub |
| `/model` | Select AI model |
| `/add-dir` | Add trusted directories |
| `/cwd` | Switch working directories mid-session |
| `/delegate` | Hand off tasks to Copilot coding agent on GitHub |
| `/agent` | Select from available custom agents |
| `/mcp add` | Configure additional MCP servers |
| `/usage` | View session statistics (premium requests, code edits, token usage) |
| `/feedback` | Submit feedback, bug reports, or feature suggestions |
| `?` | Display all available commands |

## Special Syntax

| Syntax | Description |
|--------|-------------|
| `@filepath` | Reference specific files |
| `!command` | Execute shell commands directly (bypasses AI) |
| `Esc` | Stop operations mid-execution |

## Key Features

### Agentic Capabilities
- Can edit files directly
- Can run commands
- Can create new files
- Multi-step task execution

### Session Persistence
- Maintains context within sessions
- Can resume previous sessions with `--resume` or `--continue`
- Builds on previous conversations

### MCP Support
- Extend capabilities with custom MCP servers
- `/mcp add` to configure servers

### Custom Agents & Instructions
- Load custom agents from user, repo, org, and enterprise levels
- Custom instructions from Markdown files

### GitHub Integration
- Access to GitHub repositories, issues, and PRs
- `/delegate` to hand off to GitHub's cloud agent
- Natural language queries about GitHub data

## Permissions & Safety

- Asks for approval before modifying/deleting files
- Path and URL permission systems with heuristic-based detection
- Options to approve individual commands or batch-approve for session

**Flags:**
- `--allow-all-paths` - Allow all path access
- `--allow-url` - Allow URL access

## Requirements

- Active GitHub Copilot subscription (Individual, Business, or Enterprise)
- PowerShell v6+ (Windows only)
- Organization/enterprise policies must permit CLI usage

## Comparison: Old vs New

| Feature | NEW `copilot` | OLD `gh copilot` (deprecated) |
|---------|---------------|-------------------------------|
| Status | Active | Deprecated (Oct 2025) |
| Type | Agentic assistant | Simple suggest/explain |
| Edit files | ✅ Yes | ❌ No |
| Run commands | ✅ Yes | ❌ No |
| Session persistence | ✅ Yes | ❌ No |
| MCP support | ✅ Yes | ❌ No |
| Custom agents | ✅ Yes | ❌ No |
| Models | Claude Sonnet 4.5, etc. | Limited |

## Comparison: Copilot CLI vs Claude Code

Both are now very similar agentic assistants:

| Feature | GitHub Copilot CLI | Claude Code |
|---------|-------------------|-------------|
| Agentic | ✅ Yes | ✅ Yes |
| Edit files | ✅ Yes | ✅ Yes |
| Run commands | ✅ Yes | ✅ Yes |
| Session persistence | ✅ Yes | ✅ Yes |
| MCP support | ✅ Yes | ✅ Yes |
| Custom instructions | ✅ Yes | ✅ Yes (CLAUDE.md) |
| Default model | Claude Sonnet 4.5 | Claude Sonnet |
| Permission system | ✅ Yes | ✅ Yes |
| Slash commands | ✅ Yes | ✅ Yes |
| File references | `@filepath` | Direct paths |
| Shell passthrough | `!command` | Bash tool |
| Resume sessions | `--resume`/`--continue` | `--continue` |

**Key Differences:**
- Copilot CLI integrates deeply with GitHub (issues, PRs, repos)
- Copilot CLI has `/delegate` to hand off to GitHub's cloud agent
- Claude Code has more sophisticated planning capabilities
- Different pricing (Copilot subscription vs Claude API)

## Sources

- [GitHub Copilot CLI Repository](https://github.com/github/copilot-cli)
- [GitHub Copilot CLI Docs](https://docs.github.com/en/copilot/how-tos/use-copilot-agents/use-copilot-cli)
- [GitHub Copilot CLI Features](https://github.com/features/copilot/cli)
- [Installing Copilot CLI](https://docs.github.com/en/copilot/how-tos/set-up/install-copilot-cli)
- [About Copilot CLI](https://docs.github.com/en/copilot/concepts/agents/about-copilot-cli)
