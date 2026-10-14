# Global Claude Code Rules

## OMP Harness
- When running under OMP, apply `/shake` after every 3 turns (turns 3, 6, 9, ...).

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
- Use `graft` for worktree creation and management. Cross-repo operations (e.g., `graft add-dir` across different repos) are not supported.

## Tool Preferences
- Prefer native CLIs over MCP servers when available: GitHub (`gh`), Buildkite (`bk`), Sentry (`sentry`), Google Workspace (`gws`), Atlassian Jira/Confluence (`acli`), Linear (`linear`), Datadog (`pup`), and Glean (`glean`). See the "Native CLI Preference" section below for installation and authentication commands.
- For Confluence, use `acli` (e.g., `acli confluence page view --id <PAGE_ID>`).
- For Datadog metric discovery, ask the user for the exact metric name if not found within 5 queries instead of brute-forcing.
- When Atlassian/Datadog MCP tokens expire, notify the user immediately and pause rather than retrying.

## Native CLI Preference

Native CLIs are more stable and reliable than their MCP server counterparts, and they are human-friendly too. When a native CLI is available for a service, prefer it over the equivalent MCP server.

| Service | CLI | Install | Auth | Homepage |
|---|---|---|---|---|
| GitHub | `gh` | `brew install gh` | `gh auth login` | https://cli.github.com/ |
| Buildkite | `bk` | `brew install buildkite/buildkite/bk@3` | `bk auth login` | https://github.com/buildkite/cli |
| Sentry | `sentry` | `curl https://cli.sentry.dev/install -fsS | bash` | `sentry auth login` | https://github.com/getsentry/cli |
| Google Workspace | `gws` | `gohan install gws` | `gws auth login` | https://github.com/googleworkspace/cli |
| Atlassian (Jira/Confluence) | `acli` | `brew install atlassian/acli/acli` | `acli auth login` | https://developer.atlassian.com/cloud/acli/ |
| Linear | `linear` | `brew install schpet/tap/linear` | `linear auth login` | https://github.com/schpet/linear-cli |
| Datadog | `pup` | `brew install datadog-labs/pack/pup` | `pup auth login` | https://github.com/datadog-labs/pup |
| Glean | `glean` | `brew install gleanwork/tap/glean-cli` | `glean auth login` | https://github.com/gleanwork/glean-cli |

Use the CLI first unless the user explicitly asks for the MCP server or the CLI is not available.

For Google Workspace, `gws auth setup` is the one-time project and credential setup. Subsequent sessions use `gws auth login`.

## Code Changes
- When updating model references, config values, or similar cross-cutting changes, search ALL files including test files, config files, and fallback/default values. Run `grep -r` for the old value after changes to confirm nothing was missed.
- When researching observability (Datadog, Quickwit, Sentry, etc.), always include a direct link to the source (dashboard, query, issue) alongside any text summary.
- ALWAYS write test code before pushing code to remote
- Write code comments to explain why the code exists or a non-obvious decision was made, not to restate what the code does or how it works.

## Linear/Ticket Workflows
- When asked to update a Linear ticket, ONLY modify the Linear document via MCP. Do NOT edit on-repo `specs/**/*.md` or other repo files unless explicitly requested.
- State the target scope ("editing Linear ticket X only, no repo files") before starting.

## Debugging Workflow
- Gather and cite evidence (Datadog traces, git blame, PR links, log snippets) BEFORE proposing a fix.
- Present findings as: (1) symptom + evidence links, (2) root cause + code/log citations, (3) proposed fix. STOP after (3) and wait for approval before making changes.
- Do NOT say "I'll apply the fix" until the diagnosis is confirmed.

## Search Conventions
- For literal string searches ("find all references to X"), match the EXACT string only. Do not include partial or extended matches (e.g., `X-suffix`) unless asked.

## Testing / TDD
- Confirm the target function/method name with the user before writing tests.
- Sanity-check the RED phase: verify the test failed for the RIGHT reason by inspecting output, not just the exit code. Watch for bash quoting bugs that produce false REDs.

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

For Snowflake queries, follow [snowflake-guide.md](snowflake-guide.md).

