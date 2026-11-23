---
name: setup
metadata:
  version: "0.1.0"
description: "Configure one ASDLC setup target per run (.gitignore, docs/ISSUE-TRACKING.md) through an interview."
disable-model-invocation: true
---

# Goal

Configure one setup target per run, so every developer of the project works with the same shared configuration.

# Inputs

- **Target:** Required. One row of Targets. Missing → ask, offering the Targets rows.

# Targets

| Target | Reference | Output |
|---|---|---|
| gitignore | [references/gitignore.md](references/gitignore.md) | `.gitignore` in the repository root |
| issue-tracking | [references/issue-tracking.md](references/issue-tracking.md) | `docs/ISSUE-TRACKING.md` |

# Procedure

1. Read only the selected target's Reference.
2. Follow its Procedure under Rules.

# Rules

Apply to every target.

- Output exists → read it as interview context; keep every part the interview does not change.
- Clarify the target through `interview` in Interview mode.
- Completing the output needs a decision that is deferred or unknown → report the open decisions; write nothing.
- After writing, ask one review question with the user-input tool; its preview shows the written output.
  - Like it → report the output path.
  - Wording change → edit, ask again.
  - Decision change → reopen the interview.
- Never commit.
