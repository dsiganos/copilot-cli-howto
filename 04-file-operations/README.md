# 04 - File Operations

**Time**: 30 minutes
**Level**: Intermediate

## Overview

Learn how to work with files in GitHub Copilot CLI using the `@filepath` syntax, understand the permission system, and master file editing workflows.

## The @filepath Syntax

Reference specific files in your prompts using `@`:

```bash
> @src/index.js explain this file

> @package.json what dependencies are installed?

> @README.md add a section about installation
```

### Basic Usage

```bash
# Reference a single file
> @config.yaml what settings are available?

# Reference multiple files
> @src/auth.js @src/user.js how do these interact?

# Reference with context
> Looking at @api/routes.js, add a new endpoint for /users
```

### Path Formats

```bash
# Relative paths (from current directory)
> @./src/main.js

# Absolute paths
> @/home/user/project/file.js

# Parent directory
> @../shared/utils.js

# Nested paths
> @src/components/Button/index.tsx
```

## File Reading

### View File Contents

```bash
> Show me @src/config.js

> What's in @.env.example?

> Display the contents of @docker-compose.yml
```

### Analyze Files

```bash
> @src/utils.js explain each function in this file

> @api/server.js what endpoints are defined?

> @tests/auth.test.js what test cases are covered?
```

### Compare Files

```bash
> Compare @src/old-auth.js and @src/new-auth.js

> What's different between @config.dev.json and @config.prod.json?
```

## File Editing

### Make Changes

```bash
> @src/utils.js add a function to format dates

> @README.md update the installation instructions

> @package.json add eslint as a dev dependency
```

### Review Before Applying

Copilot shows you changes before applying:

```
Proposed changes to src/utils.js:

+ export function formatDate(date) {
+   return date.toLocaleDateString('en-US', {
+     year: 'numeric',
+     month: 'long',
+     day: 'numeric'
+   });
+ }

Apply changes? (y/n)
```

### Tool Approval System

When Copilot proposes to use a tool (edit file, run command, etc.), you have **three options**:

```
Tool: Edit file src/config.js

How would you like to proceed?
  1. Approve once (just this action)
  2. Approve for session (all similar actions)
  3. Reject (don't perform this action)

Choice (1/2/3):
```

**Option details:**

- **Approve once (1)**: Approves only this specific action. You'll be prompted again for the next action.
- **Approve for session (2)**: Approves all similar tool uses for the rest of the session. Use this when you trust Copilot to make multiple similar changes.
- **Reject (3)**: Cancels this action. Copilot will not proceed with the proposed change.

**When to use each:**

```bash
# Approve once - for careful, step-by-step verification
> @src/important.js make changes
[Choose 1] - Review each change individually

# Approve for session - for batch operations you trust
> Fix typos in all @src/*.js files
[Choose 2] - Trust Copilot to fix all files

# Reject - when the proposed action is wrong
> @production.config delete this file
[Choose 3] - Don't delete important config!
```

### Undo Changes

If you approve a change you don't want:

```bash
> Undo the last change to @src/utils.js

> Revert @config.json to its previous state
```

## File Creation

### Create New Files

```bash
> Create @src/helpers/validation.js with email validation functions

> Create @tests/user.test.js with test cases for the user module

> Create @.github/workflows/ci.yml for GitHub Actions
```

### Create from Templates

```bash
> Create @src/components/Card.tsx as a React component like @src/components/Button.tsx

> Create @api/users.js following the pattern in @api/posts.js
```

## Permission System

### Trust Model

Copilot uses a permission system for file access:

- **Trusted directories**: Full read/write access
- **Untrusted directories**: Read-only or no access

### Granting Trust

When you start Copilot:

```
? Do you trust the files in /home/user/project? (y/n)
```

Or add directories during session:

```bash
> /add-dir ~/other-project
```

### Permission Flags

```bash
# Trust all paths (use carefully!)
copilot --allow-all-paths

# Allow URL access
copilot --allow-url
```

### What Requires Permission

| Action | Permission Required |
|--------|-------------------|
| Read file contents | Trust or explicit approval |
| Edit existing file | Trust or explicit approval |
| Create new file | Trust or explicit approval |
| Delete file | Always requires approval |
| Execute commands | Always requires approval |

## Multi-File Operations

### Batch Reading

```bash
> Summarize all files in @src/components/

> What do the files in @api/ do?

> Review @tests/*.test.js for coverage gaps
```

### Batch Editing

```bash
> Add copyright headers to all files in @src/

> Update imports in @src/components/ to use the new path

> Fix the typo "recieve" in all @**/*.js files
```

### Refactoring Across Files

```bash
> Rename the User class to Account in @src/models/ and update all imports

> Move @src/utils/auth.js to @src/auth/utils.js and update references

> Split @src/api.js into separate files by endpoint
```

## Advanced Patterns

### Contextual Editing

```bash
> Looking at how @src/auth.js handles errors, apply the same pattern to @src/api.js
```

### Template-Based Creation

```bash
> Based on @src/models/User.js, create @src/models/Product.js for an e-commerce product
```

### Code Generation

```bash
> Generate @src/types/api.ts with TypeScript interfaces for all endpoints in @api/
```

### Documentation Generation

```bash
> Generate @docs/API.md documenting all functions in @src/api/

> Create @src/README.md explaining the folder structure
```

## Best Practices

### 1. Be Specific About Changes

```bash
# ❌ Vague
> Fix @src/auth.js

# ✅ Specific
> @src/auth.js fix the null check on line 45 where user might be undefined
```

### 2. Review Before Approving

Always read the proposed changes before typing `y`:

```
Proposed changes to src/config.js:
- API_URL: 'http://localhost:3000'
+ API_URL: 'https://api.production.com'

Apply changes? (y/n)
```

### 3. Work Incrementally

```bash
# Instead of one big change
> Rewrite @src/auth.js completely

# Make incremental changes
> @src/auth.js first, add input validation
> Now add error handling
> Now add logging
```

### 4. Verify After Changes

```bash
> @src/auth.js show me the updated file

> Did the changes break anything?

> Run the tests for this file
```

### 5. Use Version Control

```bash
> !git diff src/auth.js  # See changes
> !git add src/auth.js   # Stage if good
> !git checkout src/auth.js  # Revert if bad
```

## Common Tasks

### Adding Functions

```bash
> @src/utils.js add a debounce function
```

### Modifying Existing Code

```bash
> @src/api.js change the timeout from 5000 to 10000
```

### Adding Comments

```bash
> @src/complex-algorithm.js add comments explaining the logic
```

### Adding Types

```bash
> @src/user.js add JSDoc type annotations
```

### Fixing Bugs

```bash
> @src/calculate.js fix the off-by-one error in the loop
```

### Adding Error Handling

```bash
> @src/api.js add try-catch blocks to all async functions
```

## Troubleshooting

### "File not found"

```bash
# Check the path
> !ls src/

# Use correct relative path
> @./src/file.js
```

### "Permission denied"

```bash
# Add the directory to trusted list
> /add-dir /path/to/directory

# Or restart with trust
copilot --allow-all-paths
```

### "File too large"

Large files may be summarized. Ask for specific sections:

```bash
> @large-file.js show me just the exports

> @large-file.js show lines 100-200
```

## Quick Reference

| Task | Syntax |
|------|--------|
| Reference file | `@filepath` |
| Read file | `Show me @file` |
| Edit file | `@file change X to Y` |
| Create file | `Create @file with...` |
| Compare files | `Compare @file1 and @file2` |
| Multiple files | `@file1 @file2 ...` |
| Directory | `@dir/` or `@dir/*` |
| Trust directory | `/add-dir path` |

## Next Steps

Now that you can work with files:

1. [05-shell-integration](../05-shell-integration/) - Run shell commands
2. [06-mcp-extensions](../06-mcp-extensions/) - Extend capabilities
3. [08-workflows](../08-workflows/) - Real-world workflows

---

**Estimated completion time**: 30 minutes
**Previous**: [03-slash-commands](../03-slash-commands/)
**Next**: [05-shell-integration](../05-shell-integration/)
