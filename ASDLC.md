# ASDLC

## How to Use ASDLC

- At the start of every session: read `HANDOFF.md` in the project root when it exists. Compare it with the repository before relying on it; if they differ, list the differences and ask the developer which is correct.
- At the start of every session, when `HANDOFF.md` does not exist: continue without it. `handoff-write` creates it when work on a feature progresses.

## Document Map

- `HANDOFF.md` (project root, not committed): short-term memory of the active feature's current work. Each checkout, including each worktree, has its own copy or none.

## Skill Map

- `handoff-write`: creates, updates, or resets `HANDOFF.md`. Invoke it at the end of every turn in which work on the active feature progressed or a review produced results, and when work on a different feature starts.
