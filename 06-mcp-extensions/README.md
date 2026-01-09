# 06 - MCP Extensions and Custom Agents

**Time**: 45 minutes
**Level**: Advanced

## Overview

Learn how to extend GitHub Copilot CLI capabilities using MCP (Model Context Protocol) servers and custom agents.

## What is MCP?

MCP (Model Context Protocol) is a standard for connecting AI assistants to external tools and data sources. With MCP, Copilot can:

- Connect to databases
- Access internal APIs
- Integrate with external services
- Use custom tools

## Adding MCP Servers

### Basic Syntax

```bash
> /mcp add <server-name>
```

### Example: Adding a Database Server

```bash
> /mcp add postgres

MCP Server 'postgres' added.
Configuration required. Enter connection details...
```

### Listing MCP Servers

```bash
> /mcp list

Active MCP Servers:
- postgres (connected)
- internal-api (connected)
- slack (disconnected)
```

### Removing MCP Servers

```bash
> /mcp remove postgres
```

## MCP Configuration

### Configuration File

MCP servers are configured in your settings:

```json
// ~/.copilot/mcp.json
{
  "servers": {
    "postgres": {
      "command": "mcp-server-postgres",
      "args": ["--connection-string", "postgresql://..."]
    },
    "custom-api": {
      "command": "node",
      "args": ["./mcp-servers/custom-api.js"]
    }
  }
}
```

### Environment Variables

```json
{
  "servers": {
    "database": {
      "command": "mcp-server-db",
      "env": {
        "DB_HOST": "localhost",
        "DB_PORT": "5432"
      }
    }
  }
}
```

## Using MCP in Conversations

Once an MCP server is connected:

```bash
> Query the database for all users created this month

[Copilot uses the postgres MCP server to run the query]

Results:
| id | name | created_at |
|----|------|------------|
| 1  | John | 2025-01-05 |
| 2  | Jane | 2025-01-08 |
```

### Example Workflows

#### Database Queries

```bash
> Show me the top 10 customers by order value

[MCP server queries database]

> Export this as a CSV file
```

#### Internal API Access

```bash
> Get the current deployment status from our CI/CD system

[MCP server calls internal API]

> Roll back to the previous version
```

## Custom Agents

### What Are Custom Agents?

Custom agents are specialized versions of Copilot with:
- Custom instructions
- Specific capabilities
- Tailored behaviors
- Domain expertise

### Agent Levels

| Level | Location | Scope |
|-------|----------|-------|
| User | `~/.copilot/agents/` | Personal |
| Repository | `.github/agents/` | Project |
| Organization | Org settings | Team |
| Enterprise | Enterprise settings | Company |

### Selecting an Agent

```bash
> /agent

Available agents:
  ❯ Default
    code-reviewer
    security-auditor
    docs-writer
    test-generator

> /agent code-reviewer
```

### Creating a Custom Agent

Create an agent configuration file:

```yaml
# ~/.copilot/agents/code-reviewer.yml
name: code-reviewer
description: Reviews code for best practices and issues
instructions: |
  You are an expert code reviewer. When reviewing code:
  1. Check for security vulnerabilities
  2. Identify performance issues
  3. Suggest readability improvements
  4. Verify error handling
  5. Check for test coverage
```

### Repository-Level Agent

```yaml
# .github/agents/project-assistant.yml
name: project-assistant
description: Knows this specific project
instructions: |
  This is a Node.js REST API using Express.
  Database: PostgreSQL with Prisma ORM
  Auth: JWT tokens
  Testing: Jest

  When making changes:
  - Follow existing code patterns
  - Add tests for new features
  - Update API documentation
```

## Custom Instructions

### What Are Custom Instructions?

Markdown files that provide context and guidelines to Copilot.

### Creating Custom Instructions

```markdown
# .github/copilot-instructions.md

## Project Overview
This is an e-commerce platform built with React and Node.js.

## Coding Standards
- Use TypeScript for all new code
- Follow ESLint configuration
- Write unit tests for all functions

## Architecture
- Frontend: React with Redux
- Backend: Express with Prisma
- Database: PostgreSQL

## Common Tasks
- API endpoints are in /api/routes/
- Components are in /src/components/
- Tests are in /__tests__/
```

### Instruction Locations

| Location | Priority | Scope |
|----------|----------|-------|
| `.github/copilot-instructions.md` | Highest | Repository |
| `~/.copilot/instructions.md` | Medium | User |
| Organization settings | Lower | Organization |

### Path-Specific Instructions

Create instructions for specific paths in your project:

```markdown
# .github/copilot-instructions/api.instructions.md
When working in the /api directory:
- Follow REST conventions
- Use proper HTTP status codes
- Include request validation
- Add rate limiting to public endpoints
```

Path-specific instructions apply when working in that directory.

### AGENTS.md File

You can also create an `AGENTS.md` file in your repository to provide additional context:

```markdown
# AGENTS.md
This file provides context about custom agents in this repository.

## Available Agents
- code-reviewer: Reviews code for quality and issues
- security-auditor: Focuses on security vulnerabilities
- test-generator: Creates comprehensive test suites

## Project Context
[Information about your project that all agents should know]
```

The `AGENTS.md` file is automatically loaded when custom agents are used.

## Building MCP Servers

### Basic MCP Server Structure

```javascript
// my-mcp-server.js
const { Server } = require('@modelcontextprotocol/sdk');

const server = new Server({
  name: 'my-custom-server',
  version: '1.0.0'
});

// Define tools
server.addTool({
  name: 'get_weather',
  description: 'Get current weather for a location',
  parameters: {
    type: 'object',
    properties: {
      location: { type: 'string' }
    }
  },
  handler: async ({ location }) => {
    // Implementation
    return { temperature: 72, conditions: 'sunny' };
  }
});

server.start();
```

### Registering Your Server

```json
// ~/.copilot/mcp.json
{
  "servers": {
    "weather": {
      "command": "node",
      "args": ["./my-mcp-server.js"]
    }
  }
}
```

## Practical Examples

### Security Auditor Agent

```yaml
# agents/security-auditor.yml
name: security-auditor
description: Focuses on security review
instructions: |
  You are a security expert. When reviewing code:

  ALWAYS check for:
  - SQL injection vulnerabilities
  - XSS vulnerabilities
  - Authentication issues
  - Authorization bypasses
  - Sensitive data exposure
  - Insecure dependencies

  Rate severity as: Critical, High, Medium, Low

  Provide specific remediation steps.
```

Usage:

```bash
> /agent security-auditor
> Review @src/api/ for security issues
```

### Documentation Writer Agent

```yaml
# agents/docs-writer.yml
name: docs-writer
description: Generates documentation
instructions: |
  You specialize in writing clear documentation.

  For functions: Include parameters, return values, examples
  For APIs: Include endpoints, methods, request/response formats
  For README: Include overview, installation, usage, examples

  Use clear, concise language. Include code examples.
```

Usage:

```bash
> /agent docs-writer
> Generate API documentation for @api/
```

### Test Generator Agent

```yaml
# agents/test-generator.yml
name: test-generator
description: Creates comprehensive tests
instructions: |
  You write thorough unit and integration tests.

  For each function:
  - Test normal cases
  - Test edge cases
  - Test error conditions
  - Test boundary values

  Use descriptive test names.
  Mock external dependencies.
  Aim for high coverage.
```

## Best Practices

### 1. Keep Instructions Focused

```yaml
# ✅ Good - focused
instructions: |
  Review code for SQL injection vulnerabilities.

# ❌ Bad - too broad
instructions: |
  Do everything perfectly.
```

### 2. Provide Context

```yaml
instructions: |
  This project uses:
  - Framework: Express.js
  - Database: PostgreSQL
  - ORM: Prisma

  Follow the existing patterns in the codebase.
```

### 3. Include Examples

```yaml
instructions: |
  When writing tests, follow this pattern:

  describe('FunctionName', () => {
    it('should handle normal input', () => {
      expect(fn('input')).toBe('expected');
    });
  });
```

### 4. Version Control Agents

Store repository agents in version control:

```
.github/
  agents/
    code-reviewer.yml
    docs-writer.yml
  copilot-instructions.md
  copilot-instructions/
    api.instructions.md
    frontend.instructions.md
AGENTS.md
```

## Troubleshooting

### MCP Server Not Connecting

```bash
# Check if server is running
> /mcp list

# Restart server
> /mcp remove server-name
> /mcp add server-name
```

### Agent Not Found

```bash
# List available agents
> /agent

# Check agent file location
ls ~/.copilot/agents/
ls .github/agents/
```

### Instructions Not Applied

- Check file location
- Verify YAML/Markdown syntax
- Restart Copilot session

## Quick Reference

| Command | Description |
|---------|-------------|
| `/mcp add <name>` | Add MCP server |
| `/mcp list` | List servers |
| `/mcp remove <name>` | Remove server |
| `/agent` | List/select agents |
| `/agent <name>` | Switch to agent |

## Next Steps

Now that you understand extensions:

1. [07-github-integration](../07-github-integration/) - GitHub integration
2. [08-workflows](../08-workflows/) - Real-world workflows
3. [09-advanced](../09-advanced/) - Advanced techniques

---

**Estimated completion time**: 45 minutes
**Previous**: [05-shell-integration](../05-shell-integration/)
**Next**: [07-github-integration](../07-github-integration/)
