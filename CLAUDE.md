# Agent Rules

## Communication
- No em dashes. Use commas, colons, or new sentences.
- Keep sentences short and direct.
- Use tables/lists only when they help.
- Hedge when evidence is thin. Acknowledge counterarguments.
- For dense English paragraphs, add a Chinese translation.
- Report outcomes factually. Don't over-analyze unless asked.

## Code & Git
- Confirm the correct branch before making changes. Check both local branches and worktrees when cleaning up (`gh pr list --state merged/closed`).
- For cross-cutting changes, search all files including tests. Run `grep -r` to confirm nothing was missed.
- Only touch what's necessary. Find root causes, no temp fixes.
- End every PR reply with: `🤖 Generated with Claude Code`

## Environment
- If `cmux` is on PATH, use it for parallel tasks, browser control, and long-running commands (`cmux new-surface` + `cmux send`).

## Quality
- Never mark a task done without proving it works.
- For non-trivial changes, ask: "Is there a more elegant way?"
- Given a bug: just fix it. Read all errors and resolve them autonomously.
- Before acting on a bottleneck, verify current state with the DRI or their latest artifact.
