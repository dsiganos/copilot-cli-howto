# 06 - Real-World Workflows

**Time**: 1 hour
**Level**: Intermediate to Advanced

## Overview

Apply GitHub Copilot CLI to real-world scenarios and daily workflows. Learn practical patterns used by developers, system administrators, and DevOps engineers.

## Developer Workflows

### Morning Routine

```bash
# 1. Check git status
gh copilot suggest "check git status and show changes"

# 2. Update dependencies
gh copilot suggest "update project dependencies safely"

# 3. Run tests
gh copilot suggest "run all tests"

# 4. Check for issues
gh copilot suggest "search code for TODO and FIXME comments"
```

### Code Review Workflow

```bash
# 1. Check out PR branch
gh copilot suggest "checkout pull request branch 123"

# 2. Show changes
gh copilot suggest "show all changes in current branch compared to main"

# 3. Run tests on changes
gh copilot suggest "run tests only for changed files"

# 4. Check code quality
gh copilot suggest "lint changed files"
```

### Debugging Workflow

```bash
# 1. Find error in logs
gh copilot suggest "search application logs for errors in last hour"

# 2. Find related code
gh copilot suggest "find files that handle authentication errors"

# 3. Check process status
gh copilot suggest "show process details for nodejs app"

# 4. Examine network
gh copilot suggest "check if port 3000 is accessible"
```

### Deployment Workflow

```bash
# 1. Build application
gh copilot suggest "build production docker image with tag"

# 2. Run tests
gh copilot suggest "run integration tests"

# 3. Push image
gh copilot suggest "push docker image to registry"

# 4. Deploy
gh copilot suggest "deploy to kubernetes production namespace"

# 5. Verify
gh copilot suggest "check deployment status and pod health"
```

## System Administration Workflows

### Server Health Check

```bash
# 1. System resources
gh copilot suggest "check CPU, memory, and disk usage"

# 2. Services status
gh copilot suggest "check status of critical services"

# 3. Recent errors
gh copilot suggest "show system errors from last hour"

# 4. Network connectivity
gh copilot suggest "test network connectivity to key services"

# 5. Generate report
gh copilot suggest "create summary report of system health"
```

### Security Audit

```bash
# 1. Failed login attempts
gh copilot suggest "show failed SSH login attempts today"

# 2. Suspicious processes
gh copilot suggest "find processes running as unusual users"

# 3. Open ports
gh copilot suggest "show all listening ports and services"

# 4. File permissions
gh copilot suggest "find world-writable files in sensitive directories"

# 5. Recent sudo commands
gh copilot suggest "show recent sudo command history"
```

### Backup Workflow

```bash
# 1. Check space
gh copilot suggest "check available space on backup drive"

# 2. Create backup
gh copilot suggest "create compressed backup of /home to /backup"

# 3. Verify backup
gh copilot suggest "verify backup integrity"

# 4. Clean old backups
gh copilot suggest "remove backups older than 30 days"

# 5. Report
gh copilot suggest "show backup file sizes and dates"
```

### Log Analysis

```bash
# 1. Find errors
gh copilot suggest "search logs for errors in last 24 hours"

# 2. Count by type
gh copilot suggest "count different error types"

# 3. Show patterns
gh copilot suggest "show most common error messages"

# 4. Timeline
gh copilot suggest "show error distribution by hour"

# 5. Export results
gh copilot suggest "save error analysis to report file"
```

## DevOps Workflows

### Docker Maintenance

```bash
# 1. Show resource usage
gh copilot suggest "show docker disk usage breakdown"

# 2. Find old containers
gh copilot suggest "list containers stopped more than 7 days ago"

# 3. Clean up safely
gh copilot suggest "remove stopped containers and unused images"

# 4. Verify services
gh copilot suggest "check all running containers are healthy"

# 5. Update images
gh copilot suggest "pull latest images for running containers"
```

### Kubernetes Troubleshooting

```bash
# 1. Find failing pods
gh copilot suggest "show pods that are not in running state"

# 2. Check pod logs
gh copilot suggest "show logs from failing pod with timestamps"

# 3. Describe pod
gh copilot suggest "show detailed pod information and events"

# 4. Check resources
gh copilot suggest "show resource usage for all pods"

# 5. Fix and verify
gh copilot suggest "restart deployment and verify all pods running"
```

### CI/CD Pipeline Debug

```bash
# 1. Check build logs
gh copilot suggest "show last build logs"

# 2. Find test failures
gh copilot suggest "extract failed test names from logs"

# 3. Check dependencies
gh copilot suggest "verify all dependencies are available"

# 4. Compare environments
gh copilot suggest "show differences between staging and production config"

# 5. Manual verification
gh copilot suggest "run same commands as CI pipeline locally"
```

## Data Science Workflows

### Data Exploration

```bash
# 1. File info
gh copilot suggest "show size and line count of all CSV files"

# 2. Preview data
gh copilot suggest "show first 10 lines of data.csv"

# 3. Check for issues
gh copilot suggest "find empty or duplicate lines in CSV"

# 4. Generate statistics
gh copilot suggest "calculate basic statistics for numeric columns"

# 5. Export subset
gh copilot suggest "extract rows matching criteria to new file"
```

### ML Training Workflow

```bash
# 1. Check resources
gh copilot suggest "check available GPU and memory"

# 2. Start training
gh copilot suggest "run python training script with GPU and log output"

# 3. Monitor progress
gh copilot suggest "watch training log in real-time"

# 4. Check results
gh copilot suggest "show model accuracy from training log"

# 5. Save artifacts
gh copilot suggest "compress and archive model files"
```

## Database Workflows

### Database Maintenance

```bash
# 1. Check connections
gh copilot suggest "show active database connections"

# 2. Database size
gh copilot suggest "show size of all databases"

# 3. Slow queries
gh copilot suggest "find slow running queries"

# 4. Backup database
gh copilot suggest "create database backup with timestamp"

# 5. Optimize
gh copilot suggest "analyze and optimize all tables"
```

### Migration Workflow

```bash
# 1. Backup before migration
gh copilot suggest "backup database before migration"

# 2. Run migration
gh copilot suggest "apply database migration scripts"

# 3. Verify schema
gh copilot suggest "compare database schema before and after"

# 4. Test queries
gh copilot suggest "run test queries on new schema"

# 5. Rollback if needed
gh copilot suggest "restore from backup if migration failed"
```

## Web Development Workflows

### Frontend Development

```bash
# 1. Install dependencies
gh copilot suggest "install npm dependencies"

# 2. Start dev server
gh copilot suggest "start development server with hot reload"

# 3. Run linter
gh copilot suggest "lint all javascript and fix auto-fixable issues"

# 4. Run tests
gh copilot suggest "run frontend tests in watch mode"

# 5. Build for production
gh copilot suggest "create optimized production build"
```

### API Development

```bash
# 1. Start local API
gh copilot suggest "start API server in development mode"

# 2. Test endpoint
gh copilot suggest "test API endpoint with curl"

# 3. Check logs
gh copilot suggest "follow API server logs"

# 4. Run API tests
gh copilot suggest "run API integration tests"

# 5. Generate docs
gh copilot suggest "generate API documentation"
```

## Performance Optimization

### Application Profiling

```bash
# 1. Identify bottleneck
gh copilot suggest "profile application and show slowest functions"

# 2. Memory analysis
gh copilot suggest "check application memory usage over time"

# 3. Database queries
gh copilot suggest "find N+1 query problems"

# 4. Network requests
gh copilot suggest "analyze network request timing"

# 5. Generate report
gh copilot suggest "create performance report with recommendations"
```

### System Optimization

```bash
# 1. Find resource hogs
gh copilot suggest "show top processes by CPU and memory"

# 2. Analyze disk I/O
gh copilot suggest "show processes with high disk I/O"

# 3. Network bottlenecks
gh copilot suggest "analyze network traffic by process"

# 4. Check system limits
gh copilot suggest "show system resource limits and current usage"

# 5. Optimize settings
gh copilot suggest "suggest system tuning parameters"
```

## Incident Response

### Production Issue

```bash
# 1. Gather info quickly
gh copilot suggest "check service status, errors, and resource usage"

# 2. Find recent changes
gh copilot suggest "show deployments in last hour"

# 3. Check logs
gh copilot suggest "extract errors from logs in last 30 minutes"

# 4. Rollback if needed
gh copilot suggest "rollback to previous deployment"

# 5. Monitor recovery
gh copilot suggest "watch service health and error rate"
```

### Post-Mortem Analysis

```bash
# 1. Timeline of events
gh copilot suggest "extract timeline of errors and deployments"

# 2. Error patterns
gh copilot suggest "analyze error patterns during incident"

# 3. Impact assessment
gh copilot suggest "calculate downtime and affected requests"

# 4. Generate report
gh copilot suggest "create incident report with all findings"
```

## Automation Scripts

### Batch Processing

```bash
# 1. List files to process
gh copilot suggest "find all unprocessed files"

# 2. Process each file
gh copilot suggest "create script to process each file"

# 3. Track progress
gh copilot suggest "log processing status for each file"

# 4. Handle errors
gh copilot suggest "move failed files to error directory"

# 5. Report results
gh copilot suggest "generate summary of processing results"
```

### Scheduled Maintenance

```bash
# 1. Stop services gracefully
gh copilot suggest "stop all services in correct order"

# 2. Perform maintenance
gh copilot suggest "run maintenance tasks"

# 3. Verify integrity
gh copilot suggest "check system integrity after maintenance"

# 4. Restart services
gh copilot suggest "start services in dependency order"

# 5. Smoke test
gh copilot suggest "run smoke tests to verify everything works"
```

## Practical Tips

### 1. Document Workflows

Save successful workflows:
```bash
# Create workflow file
echo "# Deployment Workflow" > ~/workflows/deploy.sh
gh copilot suggest "deployment workflow steps" >> ~/workflows/deploy.sh
```

### 2. Chain Commands

```bash
# Multi-step with verification
gh copilot suggest "backup database AND deploy application AND verify health"
```

### 3. Use Context

Provide relevant context in prompts:
```bash
gh copilot suggest "in Python Django project, run migrations and start server"
```

### 4. Error Recovery

Always plan for failures:
```bash
gh copilot suggest "deploy with automatic rollback on failure"
```

### 5. Dry Runs

Test destructive operations:
```bash
gh copilot suggest "show what would be deleted without actually deleting"
```

## Workflow Templates

See [examples/](./examples/) for complete workflow templates:
- [developer-day.md](./examples/developer-day.md) - Full developer workday
- [incident-response.md](./examples/incident-response.md) - Handling production issues
- [deployment.md](./examples/deployment.md) - Complete deployment workflow
- [maintenance.md](./examples/maintenance.md) - System maintenance tasks

## Next Steps

1. [07-advanced](../07-advanced/) - Advanced power user techniques
2. [08-best-practices](../08-best-practices/) - Security and best practices
3. Apply these workflows to your daily tasks

---

**Estimated completion time**: 1 hour
**Previous**: [05-aliases-shortcuts](../05-aliases-shortcuts/)
**Next**: [07-advanced](../07-advanced/)
