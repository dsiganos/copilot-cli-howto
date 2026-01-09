# 01 - Getting Started with GitHub Copilot CLI

**Time**: 15 minutes
**Level**: Beginner

## Overview

Learn how to install, authenticate, and run GitHub Copilot CLI for the first time.

## Prerequisites

Before you begin, ensure you have:

1. **GitHub Copilot subscription**
   - Individual, Business, or Enterprise plan
   - [Sign up for Copilot](https://github.com/features/copilot)

2. **Supported Platform**
   - macOS, Linux, or Windows
   - Node.js 18+ (for npm installation)

## Installation

Choose your preferred installation method:

### macOS/Linux (Homebrew)

```bash
brew install copilot-cli
```

### npm (Cross-platform)

```bash
npm install -g @github/copilot
```

### Windows (winget)

```powershell
winget install GitHub.Copilot
```

### Universal (Shell Script)

```bash
curl -fsSL https://gh.io/copilot-install | bash
```

## Verify Installation

```bash
copilot --version
```

You should see version information displayed.

## First Run

### Start Copilot CLI

```bash
copilot
```

### Authentication

On first launch, Copilot will prompt you to authenticate:

1. A browser window opens (or you'll see a URL and code)
2. Log in to your GitHub account
3. Authorize the application
4. Return to the terminal

Alternatively, authenticate directly:

```bash
copilot
> /login
```

### Trust Model

Copilot will ask you to trust the current directory:

```
? Do you trust the files in this folder? (y/n)
```

This is a security measure - Copilot can read and modify files in trusted directories.

**Options:**
- **y** - Trust this directory
- **n** - Work without file access

## Your First Conversation

Once authenticated, start chatting:

```bash
$ copilot
> Hello! What can you help me with?

GitHub Copilot CLI can help you:
- Understand and explain code
- Write and modify code
- Debug issues
- Run commands
- And much more...

> What files are in this directory?

[Copilot lists and describes the files]

> Can you explain what the main function does?

[Copilot analyzes the code and explains]
```

## Command Line Options

### Interactive Mode (Default)

```bash
copilot
```

Opens a conversational session where you can chat continuously.

### Single Prompt Mode

```bash
copilot -p "your question here"
copilot --prompt "your question here"
```

Sends a single prompt and returns the response.

### Resume Previous Session

```bash
copilot --resume
copilot --continue
```

Continues from your last conversation with full context.

### Other Options

```bash
copilot --help              # Show all options
copilot --version           # Show version
copilot --allow-all-paths   # Trust all file paths
copilot --allow-url         # Allow URL access
```

## Configuration

### View Current Settings

Copilot stores settings in your home directory. View them with:

```bash
cat ~/.config/github-copilot/config.json
```

### Model Selection

Change the AI model (default is Claude Sonnet 4.5):

```bash
copilot
> /model
```

Available models:
- Claude Sonnet 4.5 (default)
- Claude Sonnet 4
- GPT-5

## Troubleshooting

### "Authentication required"

```bash
copilot
> /login
```

Or re-run the authentication flow.

### "Copilot not found"

Ensure the installation completed and the binary is in your PATH:

```bash
# Check if installed
which copilot

# If using npm, check global modules
npm list -g @github/copilot
```

### "Subscription required"

Verify you have an active GitHub Copilot subscription at:
https://github.com/settings/copilot

### Permission Denied Errors

Run with elevated permissions:

```bash
# macOS/Linux
sudo npm install -g @github/copilot

# Or fix npm permissions
npm config set prefix ~/.npm-global
```

## Practice Exercises

Try these to get comfortable:

1. **Start a session**
   ```bash
   copilot
   ```

2. **Ask about your project**
   ```
   > What does this project do?
   ```

3. **Get help on a command**
   ```
   > How do I use git rebase?
   ```

4. **Check available commands**
   ```
   > ?
   ```

5. **Exit the session**
   ```
   > exit
   ```
   Or press `Ctrl+C`

## Quick Reference

| Action | Command |
|--------|---------|
| Start interactive mode | `copilot` |
| Single prompt | `copilot -p "prompt"` |
| Resume session | `copilot --resume` |
| Show help | `copilot --help` |
| Login | `/login` in session |
| Show commands | `?` in session |
| Exit | `exit` or `Ctrl+C` |

## Next Steps

Now that you have Copilot CLI installed and running:

1. [02-basic-usage](../02-basic-usage/) - Learn conversational interactions
2. [03-slash-commands](../03-slash-commands/) - Master slash commands
3. [04-file-operations](../04-file-operations/) - Work with files

---

**Estimated completion time**: 15 minutes
**Next**: [02-basic-usage](../02-basic-usage/)
