# 05 - Aliases and Productivity Shortcuts

**Time**: 30 minutes
**Level**: Intermediate

## Overview

Create powerful aliases and shortcuts to streamline your most common tasks with Copilot CLI.

## Essential Aliases

### Core Shortcuts

```bash
# Add to ~/.bashrc or ~/.zshrc

# Ultra-short aliases
alias cs='gh copilot suggest'
alias ce='gh copilot explain'

# Task-specific shortcuts
alias csfind='gh copilot suggest "find"'
alias csgrep='gh copilot suggest "search for"'
alias csgit='gh copilot suggest "git"'
alias csdocker='gh copilot suggest "docker"'
alias cskube='gh copilot suggest "kubernetes"'
```

## Smart Functions

### Quick Execution

```bash
# Suggest and execute immediately (use carefully!)
csx() {
    local cmd=$(gh copilot suggest "$*" --no-interaction)
    echo "Executing: $cmd"
    eval "$cmd"
}
```

### Context-Aware Shortcuts

```bash
# Git-aware suggest
gcs() {
    if git rev-parse --git-dir > /dev/null 2>&1; then
        gh copilot suggest "git $*"
    else
        echo "Not a git repository"
    fi
}

# Docker-aware suggest
dcs() {
    if command -v docker &> /dev/null; then
        gh copilot suggest "docker $*"
    else
        echo "Docker not found"
    fi
}

# Kubernetes-aware suggest
kcs() {
    if command -v kubectl &> /dev/null; then
        gh copilot suggest "kubernetes $*"
    else
        echo "kubectl not found"
    fi
}
```

### Workflow Shortcuts

```bash
# Find and explain
cse() {
    local result=$(gh copilot suggest "$*")
    echo "$result"
    gh copilot explain "$result"
}

# Suggest with history
csh() {
    local last=$(fc -ln -1)
    gh copilot suggest "$* based on: $last"
}

# Safe delete (always explain first)
csrm() {
    local cmd=$(gh copilot suggest "safely delete $*")
    gh copilot explain "$cmd"
    read -p "Execute? (y/n) " -n 1 -r
    echo
    [[ $REPLY =~ ^[Yy]$ ]] && eval "$cmd"
}
```

## Domain-Specific Shortcuts

### File Operations

```bash
alias csfind='gh copilot suggest "find files"'
alias cszip='gh copilot suggest "compress"'
alias csunzip='gh copilot suggest "extract"'
alias csmv='gh copilot suggest "move files"'
alias cscp='gh copilot suggest "copy files"'
alias csclean='gh copilot suggest "clean up files"'
```

### System Administration

```bash
alias csps='gh copilot suggest "show processes"'
alias cskill='gh copilot suggest "kill process"'
alias csmem='gh copilot suggest "check memory"'
alias csdisk='gh copilot suggest "check disk space"'
alias csport='gh copilot suggest "check port"'
alias cslog='gh copilot suggest "view logs"'
```

### Development

```bash
alias cstest='gh copilot suggest "run tests"'
alias csbuild='gh copilot suggest "build project"'
alias csdebug='gh copilot suggest "debug"'
alias cslint='gh copilot suggest "lint code"'
alias csformat='gh copilot suggest "format code"'
```

## Conditional Shortcuts

### Smart Defaults

```bash
# Suggest with context detection
csmart() {
    local context=""

    # Detect context
    if [ -f "package.json" ]; then
        context="for nodejs project"
    elif [ -f "requirements.txt" ]; then
        context="for python project"
    elif [ -f "Cargo.toml" ]; then
        context="for rust project"
    elif [ -f "pom.xml" ]; then
        context="for java project"
    fi

    gh copilot suggest "$* $context"
}
```

### Environment-Specific

```bash
# Production-safe suggestions
csprod() {
    echo "🔴 PRODUCTION MODE - Extra caution!"
    local cmd=$(gh copilot suggest "$*")
    gh copilot explain "$cmd"
    read -p "Execute in PRODUCTION? (yes/no) " confirm
    [[ "$confirm" == "yes" ]] && eval "$cmd"
}

# Development shortcuts
csdev() {
    gh copilot suggest "$* in development environment"
}
```

## Chaining Shortcuts

### Multi-Step Operations

```bash
# Find, explain, and execute
csall() {
    echo "1. Getting suggestion..."
    local cmd=$(gh copilot suggest "$*")
    echo "Command: $cmd"

    echo "\n2. Explanation:"
    gh copilot explain "$cmd"

    read -p "\n3. Execute? (y/n) " -n 1 -r
    echo
    [[ $REPLY =~ ^[Yy]$ ]] && eval "$cmd"
}
```

### Pipeline Helpers

```bash
# Suggest first command in pipeline
cs1() {
    gh copilot suggest "first command to $*"
}

# Suggest processing step
cs2() {
    local prev=$(fc -ln -1)
    gh copilot suggest "process output from: $prev"
}
```

## Clipboard Integration

### Copy Suggestions

```bash
# macOS
csc() {
    gh copilot suggest "$*" | pbcopy
    echo "✓ Copied to clipboard"
}

# Linux
csc() {
    gh copilot suggest "$*" | xclip -selection clipboard
    echo "✓ Copied to clipboard"
}

# WSL
csc() {
    gh copilot suggest "$*" | clip.exe
    echo "✓ Copied to clipboard"
}
```

### Paste and Explain

```bash
# Explain from clipboard (macOS)
cep() {
    pbpaste | xargs gh copilot explain
}

# Linux
cep() {
    xclip -selection clipboard -o | xargs gh copilot explain
}
```

## Interactive Shortcuts

### Menu-Based Selection

```bash
csmenu() {
    echo "Select task type:"
    echo "1) File operations"
    echo "2) Git operations"
    echo "3) Docker operations"
    echo "4) System admin"
    read -p "Choice: " choice

    case $choice in
        1) gh copilot suggest "file: $*" ;;
        2) gh copilot suggest "git: $*" ;;
        3) gh copilot suggest "docker: $*" ;;
        4) gh copilot suggest "system: $*" ;;
        *) echo "Invalid choice" ;;
    esac
}
```

## Practical Examples

### Daily Workflows

```bash
# Morning routine
csmorning() {
    gh copilot suggest "check system health, updates, and disk space"
}

# End of day cleanup
cscleanup() {
    gh copilot suggest "clean temporary files, old logs, and Docker resources"
}

# Project setup
cssetup() {
    local project_type="$1"
    gh copilot suggest "setup new $project_type project with best practices"
}
```

### Common Tasks

```bash
# Backup shortcut
csbackup() {
    gh copilot suggest "backup $1 to $2 safely with compression"
}

# Sync directories
cssync() {
    gh copilot suggest "sync $1 to $2 with safety checks"
}

# Monitor resource
csmonitor() {
    gh copilot suggest "monitor $* in real-time with updates"
}
```

## Performance Shortcuts

### Caching Results

```bash
# Cache last suggestion
CS_LAST_SUGGEST=""

cs_cached() {
    CS_LAST_SUGGEST=$(gh copilot suggest "$*")
    echo "$CS_LAST_SUGGEST"
}

# Reuse last suggestion
csr() {
    echo "$CS_LAST_SUGGEST"
}

# Execute cached
csre() {
    eval "$CS_LAST_SUGGEST"
}
```

## Team Shortcuts

### Shared Aliases

Create `~/team-copilot-aliases.sh`:

```bash
# Project-specific shortcuts
alias csdeploy='gh copilot suggest "deploy application to staging"'
alias cstest-all='gh copilot suggest "run all tests with coverage"'
alias csdb='gh copilot suggest "database operations"'
alias csci='gh copilot suggest "CI/CD pipeline"'
```

Share with team:
```bash
# Team members add to their shell config:
source ~/team-copilot-aliases.sh
```

## Configuration Management

### Organize by Category

Create separate files:

```bash
# ~/.config/copilot-cli/aliases/
├── git.sh          # Git-related aliases
├── docker.sh       # Docker aliases
├── system.sh       # System admin aliases
└── dev.sh          # Development aliases
```

Load in shell config:
```bash
for f in ~/.config/copilot-cli/aliases/*.sh; do
    source "$f"
done
```

## Testing Shortcuts

### Validation Function

```bash
# Test if shortcut works
test_shortcut() {
    local name="$1"
    echo "Testing $name..."

    if type "$name" &> /dev/null; then
        echo "✓ $name is defined"
        type "$name"
    else
        echo "✗ $name not found"
    fi
}

# Test all shortcuts
test_all() {
    for cmd in cs ce csx cse csall; do
        test_shortcut "$cmd"
    done
}
```

## Best Practices

1. **Keep it short**: Aim for 2-4 character aliases
2. **Make it memorable**: Use intuitive prefixes (cs, ce)
3. **Document it**: Add comments for complex functions
4. **Test first**: Validate before adding to permanent config
5. **Version control**: Keep your aliases in git
6. **Share wisely**: Only share safe, tested shortcuts

## Quick Reference

| Shortcut | Command | Use Case |
|----------|---------|----------|
| `cs` | `gh copilot suggest` | Quick suggestions |
| `ce` | `gh copilot explain` | Quick explanations |
| `csx` | Suggest and execute | Fast execution |
| `cse` | Suggest and explain | Learning mode |
| `csall` | Full workflow | Interactive mode |
| `csc` | Copy to clipboard | Share commands |

## Example Configurations

See [examples/](./examples/) for complete configuration files:
- [basic-aliases.sh](./examples/basic-aliases.sh)
- [advanced-functions.sh](./examples/advanced-functions.sh)
- [workflow-shortcuts.sh](./examples/workflow-shortcuts.sh)

## Next Steps

1. [06-workflows](../06-workflows/) - Apply shortcuts to real workflows
2. [07-advanced](../07-advanced/) - Advanced techniques
3. [08-best-practices](../08-best-practices/) - Security and best practices

---

**Estimated completion time**: 30 minutes
**Previous**: [04-shell-integration](../04-shell-integration/)
**Next**: [06-workflows](../06-workflows/)
