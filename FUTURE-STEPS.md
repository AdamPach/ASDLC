# Future Steps

Applies to: planning ASDLC work not yet started. Remove an item when it is done.

## Issue Tracker Integration

Deferred from `handoff`.

- Store the issue tracker ID and link of each work item, so AI can reference it.
- Reference the ID in commit messages, following the project's commit convention.
- Replace the work item `Status:` field with the issue tracker's status when features are pushed to the issue tracker.

## Review Skill

Deferred from `handoff`.

- Review the current changes against the active work item, using `HANDOFF.md` as input.
- Record review results through `handoff` (event Record).
- Add to `handoff` when this skill exists:
  - Statuses: Reviewed with findings (waiting for fixes) and Reviewed (no findings; waiting for developer acceptance). Implemented then waits for review instead of acceptance.
  - Record cases: reviewed with findings → Reviewed with findings, list each finding; reviewed without findings → Reviewed; implemented again → remove resolved findings.
  - Template section Review Findings: one line per finding, naming the file and the problem.

## Blocked Status

Deferred from `handoff`.

- Add status Blocked (AI cannot continue; reason in Open Threads) and its Record case when a skill can stop a work item as blocked.

## Git Context

Deferred from `handoff`.

- Decide how git context is used during implementation.
- A commit skill commits an accepted work item and invokes `handoff` (event Record, Accepted) with the commit as a detail.
