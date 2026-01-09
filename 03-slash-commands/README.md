# 03 - Slash Commands

**Time**: 30 minutes
**Level**: Beginner to Intermediate

## Overview

Master the slash commands that control GitHub Copilot CLI. These commands let you configure the tool, manage sessions, and access special features.

## Command Reference

### Quick Reference Table

| Command | Description |
|---------|-------------|
| `/login` | Authenticate with GitHub |
| `/model` | Select AI model |
| `/cwd` | Change working directory |
| `/add-dir` | Add trusted directory |
| `/delegate` | Hand off to GitHub cloud agent |
| `/agent` | Select custom agent |
| `/mcp add` | Add MCP server |
| `/usage` | View session statistics |
| `/feedback` | Submit feedback |
| `?` | Show all commands |

## Authentication

### /login

Authenticate or re-authenticate with GitHub:

```bash
> /login
```

**When to use:**
- First time setup
- Token expired
- Switching GitHub accounts
- Authentication errors

**Process:**
1. Browser opens (or URL + code displayed)
2. Log in to GitHub
3. Authorize the application
4. Return to terminal

## Model Selection

### /model

Choose which AI model to use:

```bash
> /model
```

**Available models:**
- **Claude Sonnet 4.5** (default) - Best balance of capability and speed
- **Claude Sonnet 4** - Previous generation
- **GPT-5** - OpenAI's model

**Example:**

```bash
> /model

Select a model:
  ❯ Claude Sonnet 4.5 (default)
    Claude Sonnet 4
    GPT-5

> /model claude-sonnet-4
Model changed to Claude Sonnet 4
```

**When to switch models:**
- Different models have different strengths
- Cost optimization
- Comparing outputs
- Specific task requirements

## Directory Management

### /cwd

Change the working directory mid-session:

```bash
> /cwd /path/to/new/directory
```

**Examples:**

```bash
# Switch to a different project
> /cwd ~/projects/other-app

# Go to subdirectory
> /cwd ./src

# Go to home directory
> /cwd ~
```

**When to use:**
- Working on multiple projects
- Switching contexts
- Exploring different codebases

### /add-dir

Add a directory to the trusted list:

```bash
> /add-dir /path/to/directory
```

**Examples:**

```bash
# Trust a shared library
> /add-dir ~/shared-components

# Trust a config directory
> /add-dir /etc/myapp
```

**Why trust directories?**
- Copilot needs permission to read/write files
- Untrusted directories are read-only
- Security measure against accidental modifications

## Task Delegation

### /delegate

Hand off a task to GitHub's cloud-based Copilot coding agent:

```bash
> /delegate
```

**What happens:**
1. Your current task is sent to GitHub
2. The cloud agent works on it asynchronously
3. Results appear as a PR or commit

**When to use:**
- Long-running tasks
- Complex multi-file changes
- When you need to step away
- Resource-intensive operations

**Example:**

```bash
> I need to refactor the entire authentication system to use OAuth2

> /delegate

Task delegated to Copilot coding agent.
You can track progress at: https://github.com/user/repo/copilot/tasks/123
```

## Custom Agents

### /agent

Select from available custom agents:

```bash
> /agent
```

**Agent levels:**
- **User agents** - Your personal custom agents
- **Repository agents** - Project-specific agents
- **Organization agents** - Team-wide agents
- **Enterprise agents** - Company-wide agents

**Example:**

```bash
> /agent

Available agents:
  ❯ Default
    code-reviewer (repository)
    security-auditor (organization)
    docs-writer (user)

> /agent security-auditor
Switched to security-auditor agent
```

**Creating custom agents:**
Agents are defined in configuration files. See [06-mcp-extensions](../06-mcp-extensions/) for details.

## MCP (Model Context Protocol)

### /mcp add

Add an MCP server to extend Copilot's capabilities:

```bash
> /mcp add <server-name>
```

**Examples:**

```bash
# Add a database MCP server
> /mcp add postgres-server

# Add a custom API server
> /mcp add my-internal-api
```

**What MCP enables:**
- Connect to databases
- Access internal APIs
- Integrate with external tools
- Add custom capabilities

See [06-mcp-extensions](../06-mcp-extensions/) for detailed MCP documentation.

## Session Information

### /usage

View statistics about your current session:

```bash
> /usage
```

**Output includes:**
- Premium requests used
- Token usage
- Code edits made
- Files modified
- Session duration

**Example output:**

```
Session Statistics:
- Duration: 45 minutes
- Messages: 23
- Tokens used: 15,432
- Premium requests: 3
- Files edited: 5
- Lines changed: +127 / -43
```

**Why monitor usage:**
- Track quota consumption
- Understand session complexity
- Optimize prompt efficiency

## Feedback

### /feedback

Submit feedback, bug reports, or feature suggestions:

```bash
> /feedback
```

**Opens a dialog to:**
- Report bugs
- Suggest features
- Share feedback
- Rate the experience

## Help

### ?

Display all available commands:

```bash
> ?
```

**Shows:**
- All slash commands
- Brief descriptions
- Usage hints

## Command Patterns

### Chaining Actions

```bash
> /cwd ~/new-project
> /model claude-sonnet-4
> Now let's analyze this codebase
```

### Setup Workflow

```bash
# Start of session setup
> /login                    # Ensure authenticated
> /model claude-sonnet-4.5  # Select best model
> /add-dir ~/shared-libs    # Trust shared libraries
> Ready to work!
```

### Delegation Workflow

```bash
> Refactor the payment module to support multiple currencies

[Copilot shows plan]

> This looks good, but it's a big change

> /delegate

[Task handed off to cloud agent]
```

## Tips

### 1. Check Usage Regularly

```bash
> /usage
```

Helps you understand token consumption and optimize prompts.

### 2. Use the Right Model

- **Claude Sonnet 4.5**: Complex reasoning, best quality
- **Claude Sonnet 4**: Good balance, faster
- **GPT-5**: Alternative perspective

### 3. Delegate Large Tasks

For tasks that would take many iterations:

```bash
> /delegate
```

Let the cloud agent handle it asynchronously.

### 4. Trust Only Necessary Directories

Security best practice - only trust directories you're actively working with.

### 5. Use ? When Stuck

```bash
> ?
```

Shows all available commands and options.

## Practice Exercises

1. **Check available commands**
   ```bash
   copilot
   > ?
   ```

2. **View session statistics**
   ```bash
   > /usage
   ```

3. **Change model**
   ```bash
   > /model
   # Select a different model
   > Compare this code to what you would have written before
   ```

4. **Change directory**
   ```bash
   > /cwd ~
   > What's in my home directory?
   ```

5. **Submit feedback**
   ```bash
   > /feedback
   # Share your experience
   ```

## Quick Reference

| Command | Shortcut | Purpose |
|---------|----------|---------|
| `/login` | - | Authenticate |
| `/model` | - | Change AI model |
| `/cwd <path>` | - | Change directory |
| `/add-dir <path>` | - | Trust directory |
| `/delegate` | - | Hand off to cloud |
| `/agent` | - | Select agent |
| `/mcp add` | - | Add MCP server |
| `/usage` | - | Show statistics |
| `/feedback` | - | Submit feedback |
| `?` | - | Show help |

## Next Steps

Now that you know the slash commands:

1. [04-file-operations](../04-file-operations/) - Work with files using @filepath
2. [05-shell-integration](../05-shell-integration/) - Run shell commands with !
3. [06-mcp-extensions](../06-mcp-extensions/) - Deep dive into MCP

---

**Estimated completion time**: 30 minutes
**Previous**: [02-basic-usage](../02-basic-usage/)
**Next**: [04-file-operations](../04-file-operations/)
