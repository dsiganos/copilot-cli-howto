# 01 - Getting Started with GitHub Copilot CLI

**Time**: 15 minutes
**Level**: Beginner

## Overview

Learn how to install, configure, and run your first commands with GitHub Copilot CLI.

## Prerequisites

Before you begin, make sure you have:

1. **GitHub Account** with Copilot access
   - Individual, Business, or Enterprise subscription
   - [Sign up for Copilot](https://github.com/features/copilot)

2. **GitHub CLI** installed
   - Version 2.0.0 or later
   - [Installation guide](https://github.com/cli/cli#installation)

3. **Supported Shell**
   - Bash, Zsh, Fish, or PowerShell
   - macOS, Linux, Windows (WSL), or Windows native

## Installation

### Step 1: Install GitHub CLI

#### Linux/WSL (Debian/Ubuntu)
```bash
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null
sudo apt update
sudo apt install gh
```

#### macOS
```bash
brew install gh
```

#### Windows (PowerShell)
```powershell
winget install --id GitHub.cli
```

### Step 2: Authenticate with GitHub

```bash
gh auth login
```

Follow the prompts to:
1. Choose GitHub.com
2. Select HTTPS or SSH
3. Authenticate via browser or token

### Step 3: Install Copilot CLI Extension

```bash
gh extension install github/gh-copilot
```

### Step 4: Verify Installation

```bash
gh copilot --version
```

You should see version information displayed.

## Basic Commands

GitHub Copilot CLI provides two main commands:

### 1. `gh copilot suggest` - Get Command Suggestions

Ask Copilot to suggest a command for what you want to do:

```bash
gh copilot suggest "find all pdf files in current directory"
```

**Interactive Flow**:
1. Copilot suggests a command
2. You can:
   - Execute it
   - Revise the request
   - Copy to clipboard
   - Exit

### 2. `gh copilot explain` - Explain Commands

Get explanations for complex commands:

```bash
gh copilot explain "tar -xzf archive.tar.gz -C /destination"
```

**Output**: Plain English explanation of what the command does.

## Your First Commands

### Example 1: Find Large Files

```bash
gh copilot suggest "find files larger than 100MB"
```

**Expected Suggestion**:
```bash
find . -type f -size +100M
```

### Example 2: Explain a Git Command

```bash
gh copilot explain "git rebase -i HEAD~3"
```

**Expected Explanation**:
> This command starts an interactive rebase for the last 3 commits...

### Example 3: Docker Operations

```bash
gh copilot suggest "stop all running docker containers"
```

**Expected Suggestion**:
```bash
docker stop $(docker ps -q)
```

## Understanding the Interactive Mode

When you run `gh copilot suggest`, you enter an interactive session:

```
? Select a command:
  ⦿ find . -type f -size +100M
    find . -size +100M -exec ls -lh {} \;

? What would you like to do?
  > Execute command
    Revise command
    Copy to clipboard
    Exit
```

**Options**:
- **Execute command**: Run the suggested command immediately
- **Revise command**: Refine your request with more details
- **Copy to clipboard**: Copy without executing
- **Exit**: Leave without action

## Configuration

### Check Current Settings

```bash
gh copilot config
```

### Set Preferences

```bash
# Set default shell context (bash, zsh, powershell, etc.)
gh copilot config set shell bash

# Enable/disable telemetry
gh copilot config set telemetry off
```

## Common First-Time Issues

### Issue: "extension not found"
**Solution**: Make sure you installed the extension:
```bash
gh extension install github/gh-copilot
```

### Issue: "authentication required"
**Solution**: Authenticate with GitHub:
```bash
gh auth login
```

### Issue: "copilot not available"
**Solution**: Verify you have Copilot access on your GitHub account.

## Practice Exercises

Try these commands to get comfortable:

1. **System Information**
   ```bash
   gh copilot suggest "show disk usage by directory"
   ```

2. **Process Management**
   ```bash
   gh copilot suggest "find processes using port 8080"
   ```

3. **Text Processing**
   ```bash
   gh copilot suggest "count lines in all javascript files"
   ```

4. **Explain a Command**
   ```bash
   gh copilot explain "ps aux | grep node | awk '{print $2}' | xargs kill"
   ```

## Quick Reference

| Command | Purpose | Example |
|---------|---------|---------|
| `gh copilot suggest "task"` | Get command suggestions | `gh copilot suggest "compress folder"` |
| `gh copilot explain "cmd"` | Explain a command | `gh copilot explain "rsync -avz"` |
| `gh copilot --version` | Check version | - |
| `gh copilot config` | View configuration | - |
| `gh extension upgrade gh-copilot` | Update extension | - |

## Next Steps

Now that you have Copilot CLI installed and working:

1. [02-suggest-command](../02-suggest-command/) - Deep dive into command suggestions
2. [03-explain-command](../03-explain-command/) - Master command explanations
3. [04-shell-integration](../04-shell-integration/) - Set up aliases and shell integration

## Resources

- [Official Documentation](https://docs.github.com/en/copilot/github-copilot-in-the-cli)
- [GitHub CLI Manual](https://cli.github.com/manual/)
- [Copilot FAQ](https://github.com/features/copilot)

---

**Estimated completion time**: 15 minutes
**Next**: [02-suggest-command](../02-suggest-command/)
