# 07 - Advanced Techniques and Power User Tips

**Time**: 1 hour
**Level**: Advanced

## Overview

Advanced techniques for power users. Learn to maximize efficiency, automate complex workflows, and integrate Copilot CLI deeply into your environment.

## Advanced Prompt Engineering

### Context-Rich Prompts

Instead of:
```bash
gh copilot suggest "deploy"
```

Use:
```bash
gh copilot suggest "deploy nodejs application to kubernetes production namespace with health checks and rolling update strategy, keeping 3 old replicas for quick rollback"
```

### Constraint Specification

```bash
# Specify exact constraints
gh copilot suggest "find large files but exclude node_modules, .git, and build directories, only show files larger than 100MB, sorted by size, with human readable format"
```

### Output Format Control

```bash
# Specify desired output
gh copilot suggest "list docker containers with custom format showing only name, status, and ports in table format"
```

## Programmatic Usage

### Script Integration

```bash
#!/bin/bash
# automated-deploy.sh

# Get deployment command from Copilot
DEPLOY_CMD=$(gh copilot suggest "deploy to production" --format=command)

# Log it
echo "$(date): $DEPLOY_CMD" >> deploy.log

# Execute with error handling
if eval "$DEPLOY_CMD"; then
    echo "Deployment successful"
else
    echo "Deployment failed, rolling back..."
    ROLLBACK_CMD=$(gh copilot suggest "rollback last deployment")
    eval "$ROLLBACK_CMD"
fi
```

### Pipeline Integration

```bash
# CI/CD integration
test-and-deploy() {
    local test_cmd=$(gh copilot suggest "run all tests with coverage")

    if eval "$test_cmd"; then
        echo "Tests passed, deploying..."
        local deploy_cmd=$(gh copilot suggest "deploy to staging")
        eval "$deploy_cmd"
    else
        echo "Tests failed, aborting deployment"
        return 1
    fi
}
```

## Advanced Shell Integration

### Command History Analysis

```bash
# Analyze your most used commands
analyze_commands() {
    history | awk '{print $2}' | sort | uniq -c | sort -rn | head -10 > /tmp/top_commands.txt
    gh copilot suggest "create aliases for these frequently used commands: $(cat /tmp/top_commands.txt)"
}
```

### Dynamic Alias Generation

```bash
# Generate project-specific aliases
generate_aliases() {
    local project_type=$(detect_project_type)
    gh copilot suggest "generate useful aliases for $project_type project" > .project_aliases
    source .project_aliases
}
```

### Context-Aware Prompt

```bash
# Add context to every prompt
smart_suggest() {
    local context=$(get_current_context)
    gh copilot suggest "$* [Context: $context]"
}

get_current_context() {
    local ctx=""
    [ -f "package.json" ] && ctx="$ctx nodejs"
    [ -f "requirements.txt" ] && ctx="$ctx python"
    [ -f "Dockerfile" ] && ctx="$ctx docker"
    [ -d ".git" ] && ctx="$ctx git"
    echo "$ctx"
}
```

## Multi-Step Workflows

### Workflow Orchestration

```bash
# Complex multi-step workflow
orchestrate() {
    local steps=(
        "backup database"
        "stop application services"
        "run database migration"
        "deploy new application version"
        "run smoke tests"
        "start application services"
    )

    for step in "${steps[@]}"; do
        echo "Step: $step"
        local cmd=$(gh copilot suggest "$step")
        gh copilot explain "$cmd"

        read -p "Execute? (y/n/skip all) " -n 1 -r
        echo

        if [[ $REPLY =~ ^[Yy]$ ]]; then
            eval "$cmd" || {
                echo "Step failed! Rolling back..."
                rollback
                return 1
            }
        elif [[ $REPLY =~ ^[Aa]$ ]]; then
            # Execute all remaining steps without asking
            eval "$cmd"
        else
            echo "Skipped: $step"
        fi
    done
}
```

### Conditional Execution

```bash
# Execute based on conditions
smart_execute() {
    local cmd=$(gh copilot suggest "$*")

    # Check if command is safe
    if echo "$cmd" | grep -qE 'rm |delete |drop '; then
        echo "⚠️  Potentially destructive command detected"
        gh copilot explain "$cmd"
        read -p "Are you SURE? (type 'yes'): " confirm
        [ "$confirm" != "yes" ] && return 1
    fi

    # Check if requires sudo
    if echo "$cmd" | grep -q 'sudo'; then
        echo "🔒 Command requires elevated privileges"
        read -p "Continue? (y/n): " -n 1 -r
        echo
        [[ ! $REPLY =~ ^[Yy]$ ]] && return 1
    fi

    eval "$cmd"
}
```

## Performance Optimization

### Command Caching

```bash
# Cache suggestions
declare -A COMMAND_CACHE

cached_suggest() {
    local query="$*"
    local cache_key=$(echo "$query" | md5sum | cut -d' ' -f1)

    if [ -n "${COMMAND_CACHE[$cache_key]}" ]; then
        echo "📦 From cache: ${COMMAND_CACHE[$cache_key]}"
        echo "${COMMAND_CACHE[$cache_key]}"
    else
        local result=$(gh copilot suggest "$query")
        COMMAND_CACHE[$cache_key]="$result"
        echo "$result"
    fi
}
```

### Parallel Execution

```bash
# Run multiple suggestions in parallel
parallel_suggest() {
    local queries=("$@")
    local pids=()

    for query in "${queries[@]}"; do
        (gh copilot suggest "$query" > "/tmp/cs_$$_${query//[^a-zA-Z0-9]/_}.txt") &
        pids+=($!)
    done

    # Wait for all to complete
    for pid in "${pids[@]}"; do
        wait "$pid"
    done

    # Show results
    cat /tmp/cs_$$_*.txt
    rm /tmp/cs_$$_*.txt
}

# Usage:
# parallel_suggest "find large files" "check disk space" "show running processes"
```

## Advanced Error Handling

### Retry Logic

```bash
# Retry failed commands
retry_suggest() {
    local max_attempts=3
    local attempt=1
    local cmd

    while [ $attempt -le $max_attempts ]; do
        echo "Attempt $attempt of $max_attempts"
        cmd=$(gh copilot suggest "$*")

        if eval "$cmd"; then
            return 0
        else
            echo "Failed, retrying with more context..."
            attempt=$((attempt + 1))
            sleep 2
        fi
    done

    echo "All attempts failed"
    return 1
}
```

### Fallback Strategies

```bash
# Try multiple approaches
fallback_suggest() {
    local query="$1"
    local methods=("$query" "$query with best practices" "$query step by step")

    for method in "${methods[@]}"; do
        echo "Trying: $method"
        local cmd=$(gh copilot suggest "$method")

        if [ -n "$cmd" ]; then
            echo "Success with: $method"
            echo "$cmd"
            return 0
        fi
    done

    echo "All methods failed"
    return 1
}
```

## Template Systems

### Command Templates

```bash
# Template manager
declare -A TEMPLATES

register_template() {
    local name="$1"
    local template="$2"
    TEMPLATES[$name]="$template"
}

use_template() {
    local name="$1"
    shift
    local template="${TEMPLATES[$name]}"

    # Replace placeholders
    local cmd="$template"
    local i=1
    for arg in "$@"; do
        cmd="${cmd//\$$i/$arg}"
        i=$((i + 1))
    done

    gh copilot suggest "$cmd"
}

# Register templates
register_template "deploy" "deploy \$1 application to \$2 environment with health checks"
register_template "backup" "backup \$1 to \$2 with compression and verification"

# Use templates
use_template deploy "nodejs" "production"
use_template backup "/home/user" "/backup/user"
```

## Monitoring and Logging

### Command Tracking

```bash
# Track all Copilot commands
LOG_FILE="$HOME/.copilot_history.log"

logged_suggest() {
    local query="$*"
    local timestamp=$(date '+%Y-%m-%d %H:%M:%S')
    local cmd=$(gh copilot suggest "$query")

    # Log query and result
    echo "[$timestamp] QUERY: $query" >> "$LOG_FILE"
    echo "[$timestamp] RESULT: $cmd" >> "$LOG_FILE"
    echo "---" >> "$LOG_FILE"

    echo "$cmd"
}

# View command history
alias cshistory='cat $LOG_FILE'
```

### Analytics

```bash
# Analyze usage patterns
analyze_usage() {
    echo "Most common queries:"
    grep "QUERY:" "$LOG_FILE" | cut -d: -f3- | sort | uniq -c | sort -rn | head -10

    echo "\nMost common commands:"
    grep "RESULT:" "$LOG_FILE" | cut -d: -f3- | awk '{print $1}' | sort | uniq -c | sort -rn | head -10

    echo "\nUsage over time:"
    grep "QUERY:" "$LOG_FILE" | cut -d' ' -f1 | cut -d'[' -f2 | uniq -c
}
```

## Integration with External Tools

### jq Integration

```bash
# Combine with jq for JSON processing
json_suggest() {
    local query="$*"
    gh copilot suggest "jq command to $query"
}

# Usage:
# json_suggest "extract all email addresses from users array"
```

### FZF Integration

```bash
# Interactive command selection with fzf
fzf_suggest() {
    local query="$*"
    local suggestions=$(gh copilot suggest "$query --show-all-suggestions")

    echo "$suggestions" | fzf --preview 'gh copilot explain {}' --preview-window=right:50%
}
```

### Tmux Integration

```bash
# Send suggestions to tmux pane
tmux_suggest() {
    local query="$*"
    local cmd=$(gh copilot suggest "$query")

    # Send to tmux pane
    tmux send-keys -t right "$cmd"
}
```

## Custom Modes

### Learning Mode

```bash
# Detailed explanations for everything
learning_mode() {
    export COPILOT_MODE="learning"

    alias cs='learning_suggest'
}

learning_suggest() {
    local query="$*"
    local cmd=$(gh copilot suggest "$query")

    echo "📚 Command: $cmd"
    echo "\n📖 Explanation:"
    gh copilot explain "$cmd"

    echo "\n💡 Related concepts:"
    gh copilot suggest "explain concepts in: $cmd"

    read -p "\nExecute? (y/n): " -n 1 -r
    echo
    [[ $REPLY =~ ^[Yy]$ ]] && eval "$cmd"
}
```

### Production Mode

```bash
# Extra safety for production
production_mode() {
    export COPILOT_MODE="production"
    export PS1="🔴 PRODUCTION $PS1"

    alias cs='production_suggest'
}

production_suggest() {
    echo "⚠️  PRODUCTION MODE - Extra caution!"

    local cmd=$(gh copilot suggest "$*")

    echo "Command: $cmd"
    gh copilot explain "$cmd"

    read -p "Review complete? (y/n): " -n 1 -r
    echo
    [[ ! $REPLY =~ ^[Yy]$ ]] && return 1

    read -p "Execute in PRODUCTION? (type 'EXECUTE'): " confirm
    [ "$confirm" != "EXECUTE" ] && return 1

    eval "$cmd"
}
```

## API Integration

### Custom Tool Integration

```bash
# Integrate with your own tools
my_tool_suggest() {
    local query="$*"

    # Get suggestion from Copilot
    local cmd=$(gh copilot suggest "using my-custom-tool: $query")

    # Parse and enhance
    cmd=$(echo "$cmd" | sed 's/my-tool/my-actual-tool-path/g')

    # Add standard flags
    cmd="$cmd --config ~/.mytoolrc --verbose"

    echo "$cmd"
}
```

## Advanced Examples

### Self-Optimizing Scripts

```bash
# Script that improves itself
optimize_script() {
    local script="$1"

    echo "Analyzing script: $script"
    gh copilot suggest "analyze and suggest optimizations for: $(cat $script)" > "${script}.optimized"

    echo "Optimized version saved to ${script}.optimized"
    diff "$script" "${script}.optimized"
}
```

### Intelligent Documentation

```bash
# Generate documentation from commands
document_workflow() {
    local workflow_file="$1"
    local doc_file="${workflow_file}.md"

    echo "# Workflow Documentation" > "$doc_file"
    echo "Generated: $(date)" >> "$doc_file"
    echo "" >> "$doc_file"

    while IFS= read -r cmd; do
        [ -z "$cmd" ] && continue

        echo "## Command: \`$cmd\`" >> "$doc_file"
        echo "" >> "$doc_file"
        gh copilot explain "$cmd" >> "$doc_file"
        echo "" >> "$doc_file"
    done < "$workflow_file"
}
```

## Pro Tips

1. **Chain context**: Each query can reference previous results
2. **Use templates**: Create reusable command patterns
3. **Log everything**: Track what works for future reference
4. **Build libraries**: Save successful patterns
5. **Automate learning**: Document commands you use
6. **Safety first**: Always explain before executing
7. **Optimize queries**: More context = better suggestions

## Advanced Configuration

See [examples/](./examples/) for:
- [advanced-functions.sh](./examples/advanced-functions.sh) - Complex functions
- [workflow-orchestration.sh](./examples/workflow-orchestration.sh) - Multi-step workflows
- [integration-examples.sh](./examples/integration-examples.sh) - Tool integrations

## Next Steps

1. [08-best-practices](../08-best-practices/) - Security and best practices
2. Apply advanced techniques to your workflows
3. Share your discoveries with the community

---

**Estimated completion time**: 1 hour
**Previous**: [06-workflows](../06-workflows/)
**Next**: [08-best-practices](../08-best-practices/)
