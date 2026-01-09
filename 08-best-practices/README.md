# 08 - Best Practices and Security

**Time**: 45 minutes
**Level**: All levels

## Overview

Essential best practices, security considerations, and guidelines for safe and effective use of GitHub Copilot CLI.

## Security Best Practices

### 1. Always Review Before Executing

**NEVER blindly execute suggestions**, especially:

```bash
# ❌ DANGEROUS - Don't do this
eval $(gh copilot suggest "clean up disk space")

# ✅ SAFE - Review first
gh copilot suggest "clean up disk space"
# Review the command
# Then execute manually if safe
```

### 2. Understand Destructive Commands

Always explain commands that can:
- Delete files (`rm`, `rmdir`, `shred`)
- Modify permissions (`chmod`, `chown`)
- Overwrite data (`dd`, `>`)
- Stop services (`systemctl stop`, `kill`)

```bash
# Always explain destructive commands
gh copilot explain "rm -rf /old-data/*"
# Read and understand completely before executing
```

### 3. Be Cautious with Sudo

```bash
# ⚠️  Extra caution with sudo
gh copilot suggest "install package"
# Review carefully - sudo gives full system access

# Safer approach:
gh copilot explain "sudo apt install package"
# Understand what it does first
```

### 4. Verify Remote Commands

Be especially careful with:
- Commands downloading from URLs
- Piped installations: `curl ... | bash`
- Scripts from unknown sources

```bash
# ❌ DANGEROUS
gh copilot suggest "install from script" | bash

# ✅ SAFE
gh copilot suggest "install from script"
# 1. Review the command
# 2. Check the URL
# 3. Download and inspect the script first
# 4. Then execute manually
```

### 5. Protect Sensitive Data

**NEVER** ask Copilot to:
- Generate commands with passwords, API keys, or tokens
- Process files containing sensitive information
- Suggest commands that might leak credentials

```bash
# ❌ BAD
gh copilot suggest "connect to database with password secret123"

# ✅ GOOD
gh copilot suggest "connect to database using environment variable"
# Then: export DB_PASSWORD=secret123
```

## Command Safety Checklist

Before executing any suggested command:

- [ ] Do I understand what this command does?
- [ ] Could it delete, modify, or expose data?
- [ ] Does it require elevated privileges?
- [ ] Am I in the correct directory/context?
- [ ] Do I have backups if something goes wrong?
- [ ] Is this appropriate for my environment (dev/staging/production)?

## Production Environment Guidelines

### Rule #1: Double Check Everything

```bash
# Add safety function for production
in_production() {
    [ "$ENV" = "production" ] && return 0 || return 1
}

safe_suggest() {
    if in_production; then
        echo "🔴 PRODUCTION ENVIRONMENT"
        echo "⚠️  Extra caution required"
    fi

    local cmd=$(gh copilot suggest "$*")
    echo "Command: $cmd"

    gh copilot explain "$cmd"

    if in_production; then
        read -p "Execute in PRODUCTION? (type 'yes'): " confirm
        [ "$confirm" != "yes" ] && return 1
    fi

    eval "$cmd"
}
```

### Rule #2: Use Dry Run When Available

```bash
# Always test with dry run first
gh copilot suggest "sync directories with dry run option"
# Execute dry run
# Verify results
# Then run without dry run
```

### Rule #3: Have Rollback Plans

```bash
# Always plan for rollback
gh copilot suggest "deploy application with rollback capability"

# Before major changes:
gh copilot suggest "create backup before making changes"
```

## Privacy Considerations

### What Gets Sent to GitHub

When you use Copilot CLI:
- Your prompts and commands are sent to GitHub
- Context about your command may be included
- No file contents are sent (unless explicitly included)

### Protecting Privacy

```bash
# ❌ Avoid including sensitive information
gh copilot suggest "find API key sk-abc123xyz in logs"

# ✅ Use generic terms
gh copilot suggest "find API key pattern in logs"
```

### Organizational Policies

- Follow your organization's AI usage policies
- Don't include proprietary information in prompts
- Consider using enterprise Copilot for better control
- Document when and how you use AI tools

## Development Best Practices

### 1. Start Simple, Then Iterate

```bash
# Start with broad request
gh copilot suggest "find large files"

# Refine based on result
gh copilot suggest "find large files, excluding node_modules"

# Further refine
gh copilot suggest "find large log files older than 30 days"
```

### 2. Learn from Suggestions

```bash
# Don't just execute - learn the pattern
gh copilot suggest "git branch operations"
gh copilot explain "git branch -d branch-name"

# Now you understand and can use directly
```

### 3. Document Your Workflows

```bash
# Save successful patterns
echo "# Deployment workflow" > ~/workflows/deploy.md
gh copilot suggest "deployment steps" >> ~/workflows/deploy.md
```

### 4. Version Control Your Configs

```bash
cd ~/.config/copilot-cli
git init
git add .
git commit -m "Copilot CLI configuration"
```

## Team Guidelines

### Sharing Suggestions

```bash
# ✅ Share the command and explanation
gh copilot suggest "deploy to staging"
# Copy output
# Share with team with context

# ❌ Don't share without context
# Just saying "run this command" is dangerous
```

### Code Review Practices

- Don't rely solely on Copilot for code review
- Always have human review for critical changes
- Use Copilot to help understand unfamiliar code
- Document AI-assisted decisions

### Knowledge Sharing

```bash
# Create team knowledge base
mkdir ~/team-copilot-patterns
echo "# Common Patterns" > ~/team-copilot-patterns/README.md

# Document useful patterns
gh copilot suggest "docker cleanup commands" > ~/team-copilot-patterns/docker.md
```

## Error Handling

### 1. Understand Errors

```bash
# When command fails
gh copilot explain "exit code 127"
gh copilot suggest "fix: command not found error"
```

### 2. Debug Systematically

```bash
# Step by step debugging
gh copilot suggest "check if service is running"
gh copilot suggest "check service logs for errors"
gh copilot suggest "restart service safely"
```

### 3. Don't Retry Blindly

```bash
# ❌ Bad approach
for i in {1..100}; do
    gh copilot suggest "deploy" | bash
done

# ✅ Good approach
gh copilot suggest "deploy with error handling and logging"
# Fix issues between attempts
```

## Performance Best Practices

### 1. Optimize Your Prompts

```bash
# ❌ Vague
gh copilot suggest "files"

# ✅ Specific
gh copilot suggest "find python files modified today in src directory"
```

### 2. Use Aliases for Common Tasks

```bash
# Don't repeatedly type long commands
alias csdev='gh copilot suggest --context development'
alias csprod='gh copilot suggest --context production'
```

### 3. Cache When Appropriate

```bash
# Cache commands you use frequently
CACHE_FILE=~/.copilot_cache.txt

cache_suggest() {
    if grep -q "^$*|" "$CACHE_FILE" 2>/dev/null; then
        grep "^$*|" "$CACHE_FILE" | cut -d'|' -f2-
    else
        local result=$(gh copilot suggest "$*")
        echo "$*|$result" >> "$CACHE_FILE"
        echo "$result"
    fi
}
```

## Ethical Considerations

### 1. Attribution

- Acknowledge when AI helped with commands
- Don't claim AI-generated solutions as solely your work
- Share improvements back with the community

### 2. Learning vs Dependence

```bash
# ✅ Good: Learn from Copilot
gh copilot suggest "git rebase"
gh copilot explain "git rebase main"
# Now understand rebasing

# ❌ Bad: Complete dependence
# Always asking for basic commands you should know
```

### 3. Critical Thinking

- Verify suggestions make sense
- Don't assume AI is always right
- Use your expertise to validate
- Question unusual or complex suggestions

## Common Mistakes to Avoid

### 1. Trusting Blindly

```bash
# ❌ DANGEROUS
gh copilot suggest "fix my computer" | bash

# ✅ SAFE
gh copilot suggest "diagnose system issues"
# Review, understand, then execute step by step
```

### 2. Over-Automation

```bash
# ❌ Don't automate critical decisions
alias auto-deploy='gh copilot suggest "deploy to production" | bash'

# ✅ Require human approval
deploy() {
    local cmd=$(gh copilot suggest "deploy to production")
    echo "$cmd"
    read -p "Approve? " && eval "$cmd"
}
```

### 3. Ignoring Context

```bash
# ❌ Generic
gh copilot suggest "deploy"

# ✅ Context-aware
gh copilot suggest "deploy nodejs application to kubernetes staging with rolling update"
```

### 4. Not Testing

```bash
# ❌ Skip testing
gh copilot suggest "database migration" | bash

# ✅ Test first
gh copilot suggest "test database migration in dev environment"
# Test thoroughly
# Then apply to production with backup
```

## Incident Prevention

### Before Making Changes

1. **Backup**: Create backups of critical data
2. **Test**: Test in non-production first
3. **Review**: Have commands reviewed
4. **Document**: Log what you're doing
5. **Plan**: Have rollback ready

### During Execution

1. **Monitor**: Watch logs and metrics
2. **Verify**: Check each step completes successfully
3. **Stop**: Halt immediately if issues arise
4. **Communicate**: Keep team informed

### After Changes

1. **Verify**: Confirm everything works
2. **Document**: Record what was done
3. **Review**: Analyze what worked/didn't
4. **Learn**: Update procedures

## Compliance and Governance

### Audit Trail

```bash
# Log all Copilot usage
AUDIT_LOG=~/.copilot_audit.log

audited_suggest() {
    local query="$*"
    local user=$(whoami)
    local host=$(hostname)
    local timestamp=$(date '+%Y-%m-%d %H:%M:%S')

    echo "[$timestamp] $user@$host: QUERY: $query" >> "$AUDIT_LOG"

    local cmd=$(gh copilot suggest "$query")

    echo "[$timestamp] $user@$host: RESULT: $cmd" >> "$AUDIT_LOG"
    echo "$cmd"
}
```

### Compliance Requirements

- Follow data retention policies
- Maintain audit logs if required
- Use approved AI tools only
- Document AI usage in regulated environments
- Train team on proper usage

## Quick Reference

### Safety Levels

| Risk Level | Examples | Action |
|------------|----------|--------|
| 🟢 Low | `ls`, `pwd`, `echo` | Safe to execute |
| 🟡 Medium | `git commit`, `npm install` | Review first |
| 🟠 High | `docker rm`, `systemctl restart` | Explain & review |
| 🔴 Critical | `rm -rf`, `dd`, `chmod 777` | Multiple reviews + backup |

### Security Checklist

- [ ] Understand the command
- [ ] No hardcoded secrets
- [ ] Appropriate for current environment
- [ ] Have backups if needed
- [ ] Tested in safe environment
- [ ] Team aware if impactful
- [ ] Rollback plan ready

## Resources

### Official Documentation

- [GitHub Copilot CLI Docs](https://docs.github.com/en/copilot/github-copilot-in-the-cli)
- [Security Best Practices](https://docs.github.com/en/copilot/overview-of-github-copilot/github-copilot-security)

### Community Resources

- [Discussions](https://github.com/github/gh-copilot/discussions)
- [Issue Tracker](https://github.com/github/gh-copilot/issues)

### Further Reading

- Command Line Security Best Practices
- Shell Scripting Safety Guidelines
- Production Deployment Checklists

---

## Final Thoughts

GitHub Copilot CLI is a powerful tool that can significantly boost productivity. However:

- **Always review suggestions** before executing
- **Understand what commands do** before running them
- **Exercise extra caution** in production environments
- **Protect sensitive information** in your prompts
- **Keep learning** - don't become dependent
- **Share knowledge** with your team
- **Follow security best practices** at all times

Remember: Copilot is a tool to augment your skills, not replace your judgment and expertise.

---

**Estimated completion time**: 45 minutes
**Previous**: [07-advanced](../07-advanced/)
**Congratulations!** You've completed the GitHub Copilot CLI learning guide.

---

**Return to**: [Main README](../README.md)
