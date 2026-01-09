# 08 - Real-World Workflows

**Time**: 1 hour
**Level**: Intermediate to Advanced

## Overview

Apply GitHub Copilot CLI to real-world development workflows. Learn practical patterns for debugging, refactoring, feature development, and more.

## Development Workflows

### Starting a New Feature

```bash
$ copilot

# 1. Understand the codebase
> What does this project do?
> How is the code organized?

# 2. Check for related work
> Are there any issues about user notifications?

# 3. Plan the feature
> I need to add email notifications. What files would I need to modify?

# 4. Implement
> Create @src/services/notifications.js with email notification functions

# 5. Add tests
> Create tests for the notification service

# 6. Verify
> !npm test

# 7. Create PR
> Create a PR for this feature
```

### Debugging a Bug

```bash
$ copilot

# 1. Understand the problem
> Users report login fails intermittently. Where should I look?

# 2. Check logs
> !cat logs/error.log | tail -50
> What do these errors tell us?

# 3. Find the code
> @src/auth/login.js show me the login function

# 4. Identify the issue
> I see it fails when... is that the problem?

# 5. Fix it
> @src/auth/login.js fix the race condition in the login function

# 6. Test the fix
> !npm test -- --grep "login"

# 7. Verify
> Does this fix handle all the edge cases?
```

### Code Review

```bash
$ copilot

# 1. Get PR details
> Summarize PR #123

# 2. Review changes
> What files are modified in PR #123?

# 3. Check for issues
> Review the code in PR #123 for:
> - Security issues
> - Performance problems
> - Missing error handling

# 4. Specific file review
> @src/api/users.js what changes were made and are they safe?

# 5. Test coverage
> Does PR #123 have adequate test coverage?

# 6. Provide feedback
> What feedback should I give on this PR?
```

### Refactoring

```bash
$ copilot

# 1. Identify what to refactor
> The auth module is getting complex. How should we split it?

# 2. Plan the refactoring
> What would be the steps to refactor this?

# 3. Execute step by step
> First, extract the token validation into its own file
> Now move the session management
> Update all the imports

# 4. Verify each step
> !npm test

# 5. Review the result
> Compare the before and after structure
```

## DevOps Workflows

### Deployment Workflow

```bash
$ copilot

# 1. Pre-deploy checks
> !npm test
> Are all tests passing?

# 2. Build
> !npm run build
> Any build warnings I should address?

# 3. Check deployment config
> @deploy/config.yml is this configured correctly for production?

# 4. Deploy
> What command deploys to staging?
> !./scripts/deploy.sh staging

# 5. Verify
> How do I verify the deployment succeeded?
```

### CI/CD Pipeline Debug

```bash
$ copilot

# 1. Check what failed
> The CI pipeline failed. What went wrong?

# 2. Get logs
> Show me the logs from the failed job

# 3. Identify the issue
> Why is this test failing in CI but passing locally?

# 4. Fix the issue
> @.github/workflows/ci.yml fix the environment variable issue

# 5. Verify
> Push and check the pipeline
```

### Docker Workflow

```bash
$ copilot

# 1. Review Dockerfile
> @Dockerfile is this following best practices?

# 2. Build
> !docker build -t myapp .

# 3. Debug build issues
> The build failed at step 5. What's wrong?

# 4. Run
> !docker run -p 3000:3000 myapp

# 5. Debug runtime issues
> The container exits immediately. Why?
```

## Database Workflows

### Schema Changes

```bash
$ copilot

# 1. Plan the change
> I need to add a 'status' field to the users table

# 2. Create migration
> Create a migration for adding the status field

# 3. Update models
> @src/models/user.js add the status field

# 4. Run migration
> !npm run migrate

# 5. Verify
> !npm run db:test
```

### Query Optimization

```bash
$ copilot

# 1. Find slow queries
> @src/api/reports.js this endpoint is slow. Why?

# 2. Analyze
> What indexes would help this query?

# 3. Optimize
> Rewrite this query to be more efficient

# 4. Test
> !npm run benchmark
```

## Testing Workflows

### Writing Tests

```bash
$ copilot

# 1. Identify what needs tests
> @src/utils/validation.js what functions need tests?

# 2. Generate tests
> Create comprehensive tests for the validation functions

# 3. Run tests
> !npm test

# 4. Check coverage
> !npm run coverage
> What's not covered?

# 5. Add missing tests
> Add tests for the edge cases you identified
```

### Fixing Failing Tests

```bash
$ copilot

# 1. Run tests
> !npm test

# 2. Identify failures
> What tests are failing?

# 3. Analyze
> @tests/auth.test.js why is this test failing?

# 4. Fix
> Fix the failing test (or fix the code if the test is correct)

# 5. Verify
> !npm test
```

## Documentation Workflows

### API Documentation

```bash
$ copilot

# 1. Analyze the API
> @src/api/ what endpoints exist?

# 2. Generate docs
> Generate OpenAPI/Swagger documentation for these endpoints

# 3. Create README
> Create @docs/API.md with endpoint documentation

# 4. Review
> Is this documentation complete?
```

### Code Documentation

```bash
$ copilot

# 1. Find undocumented code
> @src/utils/ which functions lack documentation?

# 2. Add docs
> Add JSDoc comments to the undocumented functions

# 3. Verify
> Are the comments accurate and helpful?
```

## Team Workflows

### Onboarding

```bash
$ copilot

# New team member exploring codebase

> What is this project?
> How is it structured?
> How do I run it locally?
> What are the main components?
> Where should I start if I want to add a feature?
```

### Knowledge Transfer

```bash
$ copilot

# Document tribal knowledge

> Explain how the payment processing works
> What are the gotchas someone new should know?
> Create a document explaining the architecture
```

## Emergency Workflows

### Production Issue

```bash
$ copilot

# 1. Assess quickly
> !kubectl get pods
> @src/api/server.js when was this last modified?

# 2. Check logs
> !kubectl logs pod-name --tail 100
> What's causing these errors?

# 3. Quick fix or rollback
> What's the fastest fix?
> !kubectl rollout undo deployment/api

# 4. Post-mortem
> What caused this and how do we prevent it?
```

### Security Incident

```bash
$ copilot

# 1. Assess
> @src/auth/ could there be a security issue here?

# 2. Find vulnerabilities
> Check for SQL injection, XSS, and auth bypasses

# 3. Fix critical issues
> Fix the SQL injection vulnerability

# 4. Audit
> What other files might have similar issues?
```

## Workflow Patterns

### The Understand-Plan-Execute Pattern

```bash
# 1. Understand
> What does this code do?

# 2. Plan
> How should I approach this change?

# 3. Execute
> Make the change

# 4. Verify
> Does this work correctly?
```

### The Incremental Change Pattern

```bash
# Small, verified steps
> First, extract this function
> !npm test
> Now, add the parameter
> !npm test
> Finally, update the callers
> !npm test
```

### The Delegate Pattern

```bash
# For large tasks
> This refactoring is complex
> /delegate
[Cloud agent handles it]
[Review the resulting PR]
```

## Tips for Effective Workflows

### 1. Start with Context

```bash
> What does this project do?
> Show me the structure
```

### 2. Verify Frequently

```bash
> !npm test
> !npm run lint
```

### 3. Work Incrementally

Small changes, frequent verification.

### 4. Use Delegation Wisely

Large, well-defined tasks are good for `/delegate`.

### 5. Document as You Go

```bash
> Add a comment explaining why we made this change
```

## Next Steps

Now that you know the workflows:

1. [09-advanced](../09-advanced/) - Advanced techniques
2. [10-best-practices](../10-best-practices/) - Best practices

---

**Estimated completion time**: 1 hour
**Previous**: [07-github-integration](../07-github-integration/)
**Next**: [09-advanced](../09-advanced/)
