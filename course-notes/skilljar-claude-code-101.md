# Claude Code 101 Concepts and Cheat Sheet

## Course Info

https://anthropic.skilljar.com/claude-code-101

## Commands Reference

`Shift + Tab`

Cycle through modes. 

`/compact`

Compacts the context window in the session up to that point.

`/clear`

Completely start from scratch with no memory of the previous session.

`/context`

Get a high level overview of context size, categories taking up the most space, and graphic visually showing the breakdown.

`claude --from-pr <PR_NUMBER>`

If you created pull requests as part of your workflow with claude, you can use this command to restore the claude session associated with writing that code and continue where you left off.

`/agents`

View agents and create new ones.

`/skills`

View a list of preconfigured skills.

`/mcp`

View a list of mcp servers.

`/hooks`

Configure hooks.

## Concepts

### Context Window

Context is Claude's working memory. Whenever you enter a prompt, Claude reads a file, runs a tool call, or receives a tool call result, it's all adding to the context window. Since there's a finite amount of space, it becomes important to optimize how you use it.

When you approach the limit, the context window is automatically compacted. Compaction summarizes important details and removes unnecessary tool call results to free up space. Note that this process can potentially lose details.

### Permissions

### Explore -> Plan -> Code -> Commit Workflow

1. Explore and Plan should be done in plan mode. Claude will read relevant files, run some web searches, and give you a plan of action. If you see any issues with the plan revise them at this stage to avoid having to undo code.
2. Select "approve" on the plan and Claude will implement it.
    - Define a success criteria. For Claude to be confident in its results, it needs to be clear on what "correct" looks like. Make this explicit when writing your plan.
    - Add tools. Tools that help Claude complete its goals remove a lot of back and forth. For example, if you're building web UIs, install the Claude in Chrome extension so Claude Code can control a browser tab and test the UI directly.
    - Include a test suite. Give Claude a test suite it can continuously validate against. Claude can even write tests for you. Before handing this off, make sure the tests are a reliable source of truth to avoid false positives.
3. Tell Claude to generate a commit message in your style.


### Managing Context

Be specific. A vague prompt might seem smaller, but it actually costs more context in the long run. Without clear instructions, Claude is forced to explore your codebase more and do its own reasoning — which takes up far more context space than a detailed prompt would.

MCP servers load all of their available tools into context by default, even when you're not using them. If you have servers configured for things unrelated to the current project, consider turning them off. 

Use subagents. Subagents run in parallel with your main agent but have a completely separate context window. For tasks where you only need the answer — like "where are the authentication endpoints located?" — a subagent does the work and returns just a summary to your main agent, keeping your primary context clean.


### Code review

Use a subagent to review code. Use session linking to restore sessions from specific pull requests when debugging.

### CLAUDE.md

The CLAUDE.md file gives Claude Code persistent memory about your project. You can place one in your home folder for general directions to apply to all projects and you can also place more specific, project-oriented ones in the root directory of projects.

Claude Code reads it automatically every time you start a session.

Things like code conventions and commonly used dev commands should go in this file. This file should live in version control.

If you have documentation in your project that you want Claude to reference, use the @ symbol with the file path.

It is best practice to start with no claude.md and only include directions you find yourself repeating. That way it doesn't take up context unless needed. 

### Tools

A Google Chrome plugin to interact with a browser tab and read an app's UI is an example of a tool used by Claude Code.

Searching the web is example of Claude making a "tool" call.

Tools use the current context, and subagents use indpendent context.

### Subagents

Claude can delegate tasks to subagents that break them down and run component tasks in parallel, improving your context management. Each subagent operates in its own isolated context window.

You can run the explore subagent without being in plan mode if you just want a general summary of your codebase without intending to make changes afterward.

Before you commit, run a subagent code reviewer to look at your work. A subagent gets a fresh pair of eyes on the codebase — it doesn't carry the bias the main agent might have from the session.

Example of running a subagent:

```
Spawn the code reviewer subagent to review the code we just created
```

You can configure subagents with pre-loaded skills.

### Skills

Skills load on demand based on the current task (not loaded automatically like CLAUDE.md)

You don't have to type commands. Claude applies them automatically.

The `/commit-push-pr skill` handles the commit, push, and PR creation all in one step. Instead of doing each manually, just run the skill and Claude takes care of it.

### MCP

Model Context Protocol (MCP) is an open standard that lets Claude Code connect to external tools and data sources. 

You can connect claude to external platforms using MCP to pull in additional information.

### Hooks

Hooks let you run commands at specific points in Claude Code's lifecycle. The key difference between hooks and everything else covered in this course is that hooks are deterministic — they always run.

1. PreToolUse — runs before a tool call
2. PostToolUse — runs after a tool call completes
3. UserPromptSubmit — runs when you submit a prompt, before Claude processes it
4. Stop — runs when Claude finishes responding
5. Notification — runs when Claude sends a notification

## Modes

### Plan Mode

Plan mode takes your prompt and uses read-only tools to analyze your codebase and research your suggested implementation. It will ask clarifying questions along the way, then return a detailed plan it can execute.

### Approval mode

Claude asks permission each time it wants to edit a file or run a command.

### Auto-accept mode

File edits are automatically approved, but commands still require your permission.

## Config Reference

### CLAUDE.md

- Place in project root for project-level context.
- Place in personal machine home folder for general personalization across all projects.

### Subagents

`<project-root>/.claude/agents/<agent-name>/AGENT.md`

You can tell claude to generate agents for you. It will need a name, description, and prompt in YAML frontmatter.

### Skills

Global:

`~/.claude/skills/<skill-name>/SKILL.md`

Project:

`<project-root>/.claude/skills/<skill-name>/SKILL.md`

The description section of this file will allow Claude to decide whether to use it.

### Hooks

`<project-root>/hooks/settings.json`