# 02 - Command Suggestions with `gh copilot suggest`

**Time**: 30 minutes
**Level**: Beginner to Intermediate

## Overview

Master the art of getting AI-powered command suggestions. Learn how to phrase requests, iterate on suggestions, and handle different types of tasks.

## What is `gh copilot suggest`?

The suggest command translates natural language requests into shell commands. It's like having an expert by your side who knows thousands of commands and their options.

## Basic Syntax

```bash
gh copilot suggest "what you want to do"
```

## How It Works

1. **You describe** what you want to accomplish in plain English
2. **Copilot analyzes** your request and system context
3. **Copilot suggests** one or more commands
4. **You choose** to execute, revise, copy, or exit

## Writing Effective Prompts

### Good Prompts

Be specific about what you want:

```bash
# Good: Specific and clear
gh copilot suggest "find all .log files modified in the last 7 days"

# Good: Includes context
gh copilot suggest "compress the backup folder with maximum compression"

# Good: Specifies output format
gh copilot suggest "list running processes sorted by memory usage"
```

### Prompts to Avoid

```bash
# Too vague
gh copilot suggest "find files"

# Ambiguous
gh copilot suggest "clean up"

# Multiple unrelated tasks
gh copilot suggest "find files and also check disk space and restart service"
```

### Tips for Better Prompts

1. **Be specific**: Include file types, time ranges, sizes, etc.
2. **One task at a time**: Break complex workflows into steps
3. **Include context**: Mention tools if you have a preference
4. **Specify format**: How do you want the output?

## Common Use Cases

### File Operations

#### Find Files

```bash
# By name pattern
gh copilot suggest "find all python files in src directory"

# By size
gh copilot suggest "find files larger than 1GB in home directory"

# By modification time
gh copilot suggest "find files modified today"

# By content
gh copilot suggest "search for TODO comments in all javascript files"
```

See [examples/file-operations.md](./examples/file-operations.md) for more.

#### Compress & Archive

```bash
# Create archive
gh copilot suggest "create a tar.gz archive of the project folder"

# Extract archive
gh copilot suggest "extract a zip file to specific directory"

# Compress with best compression
gh copilot suggest "compress large-file.log with maximum compression"
```

### System Administration

#### Process Management

```bash
# Find processes
gh copilot suggest "show all node processes with their PIDs"

# Port usage
gh copilot suggest "find what process is using port 3000"

# Resource usage
gh copilot suggest "show top 10 processes by CPU usage"
```

#### Disk Management

```bash
# Disk usage
gh copilot suggest "show disk usage for each subdirectory sorted by size"

# Free space
gh copilot suggest "check available disk space in human readable format"

# Large directories
gh copilot suggest "find the 10 largest directories"
```

See [examples/system-admin.md](./examples/system-admin.md) for more.

### Git Operations

```bash
# History
gh copilot suggest "show commits from the last week"

# Branch management
gh copilot suggest "delete all local branches that have been merged"

# Search
gh copilot suggest "find commits that modified authentication.js"

# Statistics
gh copilot suggest "show number of commits per author"
```

See [examples/git-operations.md](./examples/git-operations.md) for more.

### Docker & Kubernetes

```bash
# Docker
gh copilot suggest "remove all stopped containers"
gh copilot suggest "show logs from the last 100 lines of app container"
gh copilot suggest "list all images sorted by size"

# Kubernetes
gh copilot suggest "get all pods that are not running"
gh copilot suggest "show resource usage for all nodes"
gh copilot suggest "restart deployment named api-server"
```

See [examples/docker-k8s.md](./examples/docker-k8s.md) for more.

### Text Processing

```bash
# Count lines
gh copilot suggest "count total lines of code in python files"

# Search and replace
gh copilot suggest "replace all occurrences of old-name with new-name in text files"

# Extract data
gh copilot suggest "extract email addresses from log file"

# Format output
gh copilot suggest "convert JSON file to CSV format"
```

## Interactive Mode

When Copilot suggests a command, you enter interactive mode:

```
? Select a command:
  ⦿ find . -name "*.py" -type f
    find . -iname "*.py"

? What would you like to do?
  > Execute command
    Revise command
    Copy to clipboard
    Exit
```

### Execute Command

Runs the command immediately. **Be careful** - review the command first!

### Revise Command

Refine your request with additional details:

```
Initial: "find python files"
Revision: "only in the src directory, exclude tests"
Result: find src -name "*.py" -type f ! -path "*/tests/*"
```

### Copy to Clipboard

Copy the command without executing. Useful when you want to:
- Paste into a script
- Modify before running
- Save for later

## Advanced Prompt Techniques

### Chaining Multiple Filters

```bash
gh copilot suggest "find log files larger than 10MB modified in the last week and compress them"
```

### Specifying Tools

```bash
# If you prefer specific tools
gh copilot suggest "use rsync to backup /home to /backup"
gh copilot suggest "use awk to sum values in column 3"
```

### Output Formatting

```bash
gh copilot suggest "list files with size in human readable format sorted by size descending"
```

### Conditional Operations

```bash
gh copilot suggest "if port 8080 is in use, kill the process"
gh copilot suggest "backup database only if backup file doesn't exist"
```

## Platform-Specific Commands

Copilot is aware of your OS and suggests appropriate commands:

### Linux/macOS
```bash
gh copilot suggest "show listening ports"
# → netstat -tuln | grep LISTEN
```

### macOS
```bash
gh copilot suggest "show listening ports"
# → lsof -nP -iTCP -sTCP:LISTEN
```

### Windows
```bash
gh copilot suggest "show listening ports"
# → netstat -an | findstr LISTENING
```

## Practice Exercises

Try these progressively challenging tasks:

### Beginner

1. Find all markdown files in current directory
2. Show disk space in human-readable format
3. List the 5 most recently modified files

### Intermediate

4. Find all .log files larger than 10MB
5. Show processes using more than 500MB of memory
6. Count lines in all Python files excluding comments

### Advanced

7. Find duplicate files by comparing checksums
8. Archive files modified in last 30 days, excluding certain directories
9. Generate a report of disk usage by file type

### Solutions

Solutions are provided in [examples/exercises-solutions.md](./examples/exercises-solutions.md).

## Common Patterns

### Safe Command Execution

```bash
# List first, then delete
gh copilot suggest "find temporary files older than 30 days"
# Review the list, then:
gh copilot suggest "delete temporary files older than 30 days"
```

### Preview Before Action

```bash
# Use --dry-run or similar flags when available
gh copilot suggest "sync folders with dry run to preview changes"
```

### Incremental Refinement

Start broad, then narrow down:

```bash
1. gh copilot suggest "find large files"
2. Revise: "in the downloads folder"
3. Revise: "larger than 500MB"
4. Revise: "and show their age"
```

## Troubleshooting

### Issue: Command doesn't work as expected

**Strategy**:
1. Use `gh copilot explain` on the suggested command
2. Revise with more specific details
3. Try different phrasing

### Issue: Multiple suggestions, unsure which to use

**Strategy**:
1. Use arrow keys to select each option
2. Read the command carefully
3. Use `gh copilot explain` if unsure
4. Choose the safest/simplest option

### Issue: No good suggestions

**Strategy**:
1. Simplify your request
2. Break into smaller tasks
3. Be more specific about constraints
4. Check if you're using correct terminology

## Quick Reference

| Task Type | Example Prompt |
|-----------|----------------|
| Find files | "find all [type] files in [location]" |
| Process management | "show/kill processes [criteria]" |
| Disk operations | "show disk usage for [location]" |
| Compress | "compress [file/folder] with [options]" |
| Git operations | "show/find [what] in git history" |
| Docker | "list/remove/show [resource] [criteria]" |
| Text processing | "count/extract/replace [what] in [where]" |

## Tips for Success

1. **Start simple**: Get comfortable with basic commands first
2. **Review before executing**: Always understand what a command does
3. **Use explain**: When in doubt, explain the suggested command
4. **Iterate**: Use revise to refine suggestions
5. **Learn from suggestions**: Study the commands Copilot suggests

## Next Steps

1. [03-explain-command](../03-explain-command/) - Learn to understand complex commands
2. [04-shell-integration](../04-shell-integration/) - Set up convenient aliases
3. [06-workflows](../06-workflows/) - Apply suggestions to real-world scenarios

## Additional Resources

- [Example prompts](./examples/)
- [Official documentation](https://docs.github.com/en/copilot/github-copilot-in-the-cli/using-github-copilot-in-the-cli)

---

**Estimated completion time**: 30 minutes
**Previous**: [01-getting-started](../01-getting-started/)
**Next**: [03-explain-command](../03-explain-command/)
