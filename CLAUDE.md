# Global Claude Code Rules

## Writing and Communication Style
- NEVER use em dashes. Use commas, parentheses, colons, or separate sentences instead.
- NEVER append new lines within the same sentence in text-based paragraphs.
- Prefer short sentences over complex ones.
- USE lists and tables where they improve clarity.
- Hedge appropriately where evidence is thin.
- Acknowledge counterarguments.

## Git Operations
- When cleaning up git branches, always check for both local branches AND worktrees associated with merged/closed PRs. Use `gh pr list --state merged` and `gh pr list --state closed` to identify candidates.
- Always work on the correct branch (usually `main` or `master`) unless explicitly told otherwise. Confirm which branch before making changes, especially when worktrees are involved.
- For git operations: always check for unstaged changes and handle them before pulling/rebasing. Use `git stash` or commit changes first without asking unless conflicts are unavoidable.

## Tool Usage Guidelines
- When searching for users, metrics, or resources across tools (Datadog, GitHub, etc.), limit exploration to 5-10 attempts max. If not found, ask the user for clarification rather than exhaustively trying variations.

## Tool Preferences
- For Confluence/internal docs, ALWAYS use the Glean MCP tool first (not API credentials)
- For Datadog metric discovery, ask the user for the exact metric name if not found within 5 queries instead of brute-forcing
- When Atlassian/Datadog MCP tokens expire, notify the user immediately and pause rather than retrying

## Code Changes
- When updating model references, config values, or similar cross-cutting changes, search ALL files including test files, config files, and fallback/default values. Run `grep -r` for the old value after changes to confirm nothing was missed.
- When researching observability (Datadog, Quickwit, Sentry, etc.), always include a direct link to the source (dashboard, query, issue) alongside any text summary.
- ALWAYS write test code before pushing code to remote

## PR Comments
When replying to PR comments, add agent attribution line at the end of the response

## Terminal Environment
When the `cmux` CLI is available on PATH, use it to:
- Spawn new workspaces, tabs, or panes for parallel shell tasks
- Control the built-in browser (open URLs, navigate, etc.)
- Leverage any other cmux-specific features when relevant
- For long-running Bash commands, consider spawning them in a cmux tab
  via `cmux new-surface` + `cmux send` so they're visible and manageable.

## Core Principles
- **Simplicity First:** Make every change as simple as possible. Impact minimal code.
- **Be Laziness-Free:** Find root causes. No temporary fixes. Senior developer thought.
- **Minimal Impact:** Changes should only touch what's necessary. Avoid introducing bugs.
