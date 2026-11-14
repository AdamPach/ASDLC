# Future Steps

Applies to: planning ASDLC work not yet started. Remove an item when it is done.

## Setup Skill

The `setup` skill configures a project that adopts ASDLC. It must include:

- **Ignore entry for the handoff file:** Create the project's `.gitignore` when it does not exist, and add `HANDOFF.md` to it when it is not listed. `.gitignore` is committed and shared by every developer of the project, so the change is part of setup, not of `handoff-write`.

Memo: when the `setup` skill is created, it generates the `.gitignore` entry above. Until then, `handoff-write` does not edit ignore files.

## Issue Tracker Integration

Deferred from `handoff-write`.

- Store the issue tracker ID and link of each work item, so AI can reference it.
- Reference the ID in commit messages, following the project's commit convention.
- Replace the work item `Status:` field with the issue tracker's status when features are pushed to the issue tracker.

## Review Skill

Deferred from `handoff-write`.

- Review the current changes against the active work item, using `HANDOFF.md` as input.
- Write review results into the review section of `HANDOFF.md` through `handoff-write`.
