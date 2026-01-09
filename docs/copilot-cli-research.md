# GitHub Copilot CLI Research

> This document contains research about the NEW GitHub Copilot CLI tool (the `copilot` command).

## Overview

GitHub Copilot CLI is an **agentic AI assistant** that brings AI-powered coding assistance directly to your terminal. It's powered by the same agentic technology as GitHub's Copilot coding agent.

**Important:** This is NOT the same as the old `gh copilot` extension (which was deprecated October 25, 2025).

## Installation

```bash
# macOS/Linux
brew install copilot-cli
# Prerelease:
brew install copilot-cli@prerelease

# npm (requires Node.js 22+)
npm install -g @github/copilot
# Prerelease:
npm install -g @github/copilot@prerelease

# Windows
winget install GitHub.Copilot
# Prerelease:
winget install GitHub.Copilot.Prerelease

# Universal
curl -fsSL https://gh.io/copilot-install | bash
# With custom directory and version:
curl -fsSL https://gh.io/copilot-install | VERSION="v0.0.369" PREFIX="$HOME/custom" bash

# Direct download from releases
# https://github.com/github/copilot-cli/releases
```

## Authentication

```bash
# Interactive OAuth flow
copilot
> /login

# Using Personal Access Token (PAT)
# Create PAT at: https://github.com/settings/personal-access-tokens/new
# Enable "Copilot Requests" permission
export GH_TOKEN="your-token-here"
# or
export GITHUB_TOKEN="your-token-here"
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

# Other options
copilot --allow-all-paths      # Trust all file paths
copilot --allow-all-urls       # Allow all URL access
copilot --allow-url <domain>   # Allow specific domain
copilot --agent=<name>         # Use specific custom agent
copilot --banner               # Show animated banner
copilot --version              # Show version
copilot --help                 # Show help

# Help subcommands
copilot help config            # Configuration details
copilot help environment       # Environment variables
copilot help logging           # Logging configuration
copilot help permissions       # Permission settings
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
| `@filepath` | Reference specific files (supports Tab completion) |
| `!command` | Execute shell commands directly (bypasses AI) |
| `Esc` | Stop operations mid-execution |

### File Reference Features
- **Tab completion**: Press Tab after `@` to auto-complete file paths
- **Arrow key navigation**: Use ↑↓ arrows to navigate menus (model selection, etc.)
- **Esc**: Cancel current selection or operation

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

**Agent Locations:**
- User: `~/.copilot/agents/`
- Repository: `.github/agents/`
- Organization: Org settings
- Enterprise: Enterprise settings

**AGENTS.md Support:**
- Create `AGENTS.md` in repository root for agent context
- Automatically loaded when custom agents are used

### Custom Instructions Files (Equivalent of CLAUDE.md)

| Scope | Location |
|-------|----------|
| Repository-wide | `.github/copilot-instructions.md` |
| Path-specific | `.github/copilot-instructions/**/*.instructions.md` |
| User-level | `~/.copilot/instructions.md` |

**Comparison with Claude Code:**

| Feature | Claude Code | Copilot CLI |
|---------|-------------|-------------|
| Main file | `CLAUDE.md` | `.github/copilot-instructions.md` |
| Location | Project root | `.github/` directory |
| Path-specific | `folder/CLAUDE.md` | `.github/copilot-instructions/path.instructions.md` |
| User-level | `~/.claude/` | `~/.copilot/instructions.md` |

### GitHub Integration
- Access to GitHub repositories, issues, and PRs
- `/delegate` to hand off to GitHub's cloud agent
- Natural language queries about GitHub data

## Permissions & Safety

### Tool Approval System

When Copilot proposes to use a tool (edit file, run command, etc.), three options:
1. **Approve once** - Just this action
2. **Approve for session** - All similar actions in this session
3. **Reject** - Don't perform this action

### URL Permissions

- **By default, all URL access requires approval**
- Use `--allow-all-urls` to allow all URLs (use carefully!)
- Use `--allow-url <domain>` to allow specific domains

### Path Detection

- Copilot has **limitations in automatically detecting file paths** in prompts
- **Always use `@filepath` syntax** for reliable file references
- Path detection may fail for:
  - Paths without file extensions
  - Paths in long sentences
  - Ambiguous references
  - Paths with spaces/special characters

### Permission Flags

- `--allow-all-paths` - Allow all path access
- `--allow-all-urls` - Allow all URL access
- `--allow-url <domain>` - Allow specific domain

## Requirements

- Active GitHub Copilot subscription (Individual, Business, or Enterprise)
- Node.js 22+ (for npm installation)
- PowerShell v6+ (Windows only)
- Organization/enterprise policies must permit CLI usage

## Configuration

- Config directory: `~/.copilot/`
- Main config file: `~/.copilot/config.json`
- Can be customized with `XDG_CONFIG_HOME` environment variable
- MCP servers: `~/.copilot/mcp.json`

## Usage Quota

- **Monthly quota for premium requests**
- Premium requests use advanced model capabilities
- Check with `/usage` command
- Tips to conserve: use concise prompts, break tasks into smaller pieces

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
