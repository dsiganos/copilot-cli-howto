# 02 - Basic Usage

**Time**: 30 minutes
**Level**: Beginner

## Overview

Learn how to have productive conversations with GitHub Copilot CLI. Master the interactive interface, prompting techniques, and context management.

## Interactive Mode

### Starting a Session

```bash
copilot
```

You'll see a prompt where you can type:

```
>
```

### Basic Conversation

```bash
$ copilot
> What is this project?

This appears to be a Node.js web application that...

> Can you show me the main entry point?

The main entry point is in src/index.js which...

> What dependencies does it use?

Looking at package.json, the main dependencies are...
```

### Context Awareness

Copilot remembers your conversation within a session:

```bash
> Show me the user authentication code

[Shows auth code]

> What security issues do you see in it?

[Analyzes the code you just discussed]

> Can you fix the issue you mentioned?

[Edits the file based on the conversation context]
```

## Prompting Techniques

### Be Specific

```bash
# ❌ Too vague
> fix the bug

# ✅ Specific
> fix the null pointer exception in the login function in src/auth.js
```

### Provide Context

```bash
# ❌ No context
> add validation

# ✅ With context
> add email validation to the registration form in components/RegisterForm.tsx
```

### Ask Step by Step

For complex tasks, break them down:

```bash
> First, explain how the payment system works

[Copilot explains]

> Now, what changes would we need to add refund support?

[Copilot outlines changes]

> Let's implement the refund endpoint first

[Copilot implements]
```

### Use Examples

```bash
> Create a function that formats dates like "January 1, 2025"

> The output should look like:
> - "December 25, 2024"
> - "March 15, 2025"
```

## Single Prompt Mode

For quick, one-off questions:

```bash
# Using -p flag
copilot -p "explain what docker-compose.yml does"

# Using --prompt
copilot --prompt "how do I undo the last git commit?"
```

The response is printed and Copilot exits.

### When to Use Single Prompt

- Quick questions
- Scripting and automation
- Simple explanations
- One-off commands

### When to Use Interactive Mode

- Complex tasks
- Multi-step workflows
- Code refactoring
- Debugging sessions

## Session Management

### Resume Previous Session

Continue where you left off:

```bash
copilot --resume
```

Or:

```bash
copilot --continue
```

This restores:
- Conversation history
- Context about files discussed
- Previous decisions made

### Exit a Session

```bash
> exit
```

Or press `Ctrl+C`

## Working with Responses

### Request Different Formats

```bash
> Explain this code in simple terms

> Now give me a technical explanation

> Can you summarize that in bullet points?

> Show me as a table
```

### Ask for Alternatives

```bash
> Implement a sort function

[Copilot implements]

> Show me a different approach

> What about using a library instead?
```

### Request Explanations

```bash
> Why did you choose that approach?

> What are the trade-offs?

> Are there any edge cases I should worry about?
```

## Common Tasks

### Understanding Code

```bash
> What does this file do?
> Explain the main function
> How does the authentication flow work?
> What design patterns are used here?
```

### Writing Code

```bash
> Write a function to validate email addresses
> Create a REST endpoint for user registration
> Add error handling to this function
> Implement the missing test cases
```

### Debugging

```bash
> Why is this test failing?
> What's causing the memory leak?
> Debug this error: [paste error message]
> Find the bug in this function
```

### Refactoring

```bash
> Refactor this function to be more readable
> Split this file into smaller modules
> Convert this to async/await
> Apply the DRY principle to this code
```

### Documentation

```bash
> Add JSDoc comments to this file
> Generate a README for this project
> Document the API endpoints
> Explain how to set up this project
```

## Tips for Effective Use

### 1. Be Conversational

Copilot understands natural language:

```bash
> I'm trying to add user authentication but I'm not sure where to start
> The tests are passing locally but failing in CI, any ideas?
> This code works but it's really slow, can you optimize it?
```

### 2. Reference Previous Context

```bash
> Going back to the auth code we discussed...
> Remember the bug you found earlier?
> Can you apply that same pattern here?
```

### 3. Iterate

Don't expect perfection on the first try:

```bash
> [First attempt]

> That's close, but can you also handle the edge case where...

> Actually, let's use a different approach...
```

### 4. Ask for Verification

```bash
> Does this look correct?
> Are there any issues with this approach?
> What could go wrong?
```

### 5. Request Tests

```bash
> Write tests for the function you just created
> Add edge case tests
> Show me how to test this manually
```

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Enter` | Send message |
| `Esc` | Cancel current operation |
| `Ctrl+C` | Exit session |
| `↑` / `↓` | Navigate history (if supported) |

## Common Patterns

### The Explain-Then-Modify Pattern

```bash
> First, explain what this code does
[Understanding]

> Now, modify it to also handle...
[Modification with context]
```

### The Plan-Then-Execute Pattern

```bash
> What steps would we need to add caching?
[Planning]

> Let's start with step 1
[Execution]
```

### The Review Pattern

```bash
> Review this code for issues
[Review]

> Fix the issues you found
[Fixes]

> Are there any other improvements?
[Additional suggestions]
```

## Practice Exercises

1. **Start a session and explore**
   ```bash
   copilot
   > What interesting things can you tell me about the current directory?
   ```

2. **Ask about a specific file**
   ```bash
   > Explain the purpose of package.json
   ```

3. **Request a code change**
   ```bash
   > Add a comment at the top of README.md explaining this project
   ```

4. **Use single prompt mode**
   ```bash
   copilot -p "what is the difference between git merge and git rebase?"
   ```

5. **Practice iteration**
   ```bash
   > Write a hello world function
   > Make it accept a name parameter
   > Add input validation
   > Add a docstring
   ```

## Next Steps

Now that you understand basic usage:

1. [03-slash-commands](../03-slash-commands/) - Master slash commands
2. [04-file-operations](../04-file-operations/) - Work with files
3. [05-shell-integration](../05-shell-integration/) - Run shell commands

---

**Estimated completion time**: 30 minutes
**Previous**: [01-getting-started](../01-getting-started/)
**Next**: [03-slash-commands](../03-slash-commands/)
