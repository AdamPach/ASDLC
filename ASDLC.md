# ASDLC

## How to Use ASDLC

- At the start of every session: invoke `handoff` with event Resume.
- During implementation: invoke `handoff` at each moment the Skill Map lists for it.

## Document Map

- `HANDOFF.md` (project root, not committed): short-term memory of where the active feature's implementation stands. Each checkout, including each worktree, has its own copy or none.

## Skill Map

- `handoff`: starts, resumes, or records the active feature's implementation state in `HANDOFF.md`. Invoke it at session start (Resume), when implementation of a feature starts (Start), and when a work item is implemented or accepted, or the developer asks for the next work item (Record).
