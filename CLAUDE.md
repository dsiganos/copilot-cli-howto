# Project Context for Claude Code

## Project Overview

This is a learning resource for GitHub Copilot CLI. The project needs to be updated to reflect the **new** GitHub Copilot CLI tool.

## CRITICAL: Two Different Tools Exist

### 1. NEW: GitHub Copilot CLI (`copilot` command) - CURRENT

This is the **new agentic CLI** that is very similar to Claude Code.

**Installation:**
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

**Key Features:**
- Started with `copilot` command
- Agentic assistant (can edit files, run commands)
- Session persistence within and across sessions
- MCP (Model Context Protocol) support
- Default model: Claude Sonnet 4.5 (also supports Claude Sonnet 4, GPT-5)
- Permission system for file modifications
- Custom agents and instructions support

**Slash Commands:**
- `/login` - Authenticate to GitHub
- `/model` - Select model (Claude Sonnet 4.5, Claude Sonnet 4, GPT-5)
- `/add-dir` - Add trusted directories
- `/cwd` - Switch working directories mid-session
- `/delegate` - Hand off tasks to Copilot coding agent on GitHub
- `/agent` - Select from available custom agents
- `/mcp add` - Configure additional MCP servers
- `/usage` - View session statistics (premium requests, code edits, token usage)
- `/feedback` - Submit feedback, bug reports, or feature suggestions
- `?` - Display all available commands

**Special Syntax:**
- `@filepath` - Reference specific files
- `!command` - Execute shell commands directly (bypass model)
- `--resume` / `--continue` - Resume previous sessions
- `Esc` - Stop operations mid-execution

**Permissions & Safety:**
- Asks for approval before modifying/deleting files
- Path and URL permission systems
- Flags: `--allow-all-paths`, `--allow-url`

**Custom Instructions:**
- Supports custom instructions from Markdown files (similar to CLAUDE.md)
- Can load custom agents from user, repository, organization, and enterprise levels

**Sources:**
- Repository: https://github.com/github/copilot-cli
- Docs: https://docs.github.com/en/copilot/how-tos/use-copilot-agents/use-copilot-cli
- Features: https://github.com/features/copilot/cli

### 2. OLD: `gh copilot` extension - DEPRECATED

**Status: DEPRECATED as of October 25, 2025**

This was a simple GitHub CLI extension for command suggestions and explanations.

**Commands (deprecated):**
- `gh copilot suggest "query"` - Get command suggestions
- `gh copilot explain "command"` - Explain a command

**Limitations (why it was replaced):**
- Could NOT edit files
- Could NOT run commands
- No session persistence
- No MCP support
- Stateless (each command independent)

## Project Status

**Current state of this repository:**
- The content was written about the OLD `gh copilot` tool
- Needs to be updated to cover the NEW `copilot` CLI
- The comparison document (CLAUDE-CODE-COMPARISON.md) needs major revision

## What Needs Updating

1. **README.md** - Update to describe the new `copilot` command
2. **01-getting-started/** - New installation instructions
3. **02-suggest-command/** - This concept has changed; now it's conversational
4. **03-explain-command/** - Still relevant but works differently
5. **04-shell-integration/** - New slash commands and features
6. **05-aliases-shortcuts/** - May need revision
7. **06-workflows/** - Update for agentic capabilities
8. **07-advanced/** - MCP servers, custom agents, etc.
9. **08-best-practices/** - Still relevant
10. **CLAUDE-CODE-COMPARISON.md** - Major revision needed (tools are now very similar!)

## Comparison: New Copilot CLI vs Claude Code

Both tools are now very similar agentic assistants:

| Feature | GitHub Copilot CLI | Claude Code |
|---------|-------------------|-------------|
| Agentic | ✅ Yes | ✅ Yes |
| Edit files | ✅ Yes | ✅ Yes |
| Run commands | ✅ Yes | ✅ Yes |
| Session persistence | ✅ Yes | ✅ Yes |
| MCP support | ✅ Yes | ✅ Yes |
| Custom instructions | ✅ Yes | ✅ Yes (CLAUDE.md) |
| Default model | Claude Sonnet 4.5 | Claude Sonnet 4 |
| Permission system | ✅ Yes | ✅ Yes |
| Slash commands | ✅ Yes | ✅ Yes |
| File references | `@filepath` | Direct paths |
| Shell passthrough | `!command` | Bash tool |
| Resume sessions | `--resume`/`--continue` | `--continue` |

**Main differences:**
- Copilot CLI integrates with GitHub (issues, PRs, repos)
- Copilot CLI has `/delegate` to hand off to GitHub's cloud agent
- Claude Code has more sophisticated planning capabilities
- Different pricing models (Copilot subscription vs Claude API)

## Repository URL

https://github.com/dsiganos/copilot-cli-howto
