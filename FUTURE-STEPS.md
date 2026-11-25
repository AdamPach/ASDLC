# Future Steps

Applies to: planning ASDLC work not yet started. Items are listed in the order they are to be done; each item states what it requires. Remove an item when it is done.

## Work-load Skill

Closes gaps found in the review of the implementation skills.

- `work-load`: loads a feature from the issue tracker or its request folder and invokes `handoff` with event Start, so the implementation of a feature always starts through one explicit entry point.
- Only the developer invokes it, via `/work-load`; excluded from the Skill Map in `ASDLC.md`.
- Feature tracker link or ID not supplied → run Find Features, list the features whose work items are not all Done, and let the developer choose.
- No `docs/ISSUE-TRACKING.md` → load the feature from its request folder; not named → list the request folders that have an implementation plan and work items not all Done, and let the developer choose.
- Add Load Feature to the Tracker part of `handoff`'s Document Access: Start needs it to find the implementation plan and the feature name.
- Remove the Start moment from `handoff`'s entry in the Skill Map of `ASDLC.md` and from `handoff`'s description, so AI never invokes Start on its own.
- Point `feature-push`'s Report to it.

## Tracker Document Updates

Found in the review of the implementation skills.

- After `feature-push`, the feature document, implementation plan, and work items exist only in the issue tracker. `feature-write` and `feature-plan` work only on the local request folder, and `feature-plan` stops when an implementation plan exists, so no skill can change a pushed document.
- Decide how a pushed document is changed: the feature skills read and write the tracker through the Update Operations in `docs/ISSUE-TRACKING.md`, or a skill pulls the documents back into a local request folder.
- Requires: Work-load Skill.

## Linked Material in the Tracker

Deferred from `feature-push`.

- Push the local files that pushed documents link (mockups, designs) to the issue tracker, and rewrite their links. Until then, `feature-push` deletes them with the request folder, and work items whose Appearance depends on them cannot be implemented as specified.
- Requires an attachment Operation in `docs/ISSUE-TRACKING.md`, defined by `setup`.

## Implement Skill

Deferred from `handoff`.

- Implement the active work item; invoke `handoff` with event Record when AI stops before the work item is implemented and tested, and when it is implemented and tested.
- Add the stop moment to `handoff`'s entry in the Skill Map of `ASDLC.md`.
- Define what AI verifies before Implemented ("tested"); the work item's acceptance criteria are manual checks the developer performs.
- Route the developer's answers to Open Threads that change the feature or implementation plan through Tracker Document Updates.
- Requires: Tracker Document Updates; Linked Material in the Tracker.

## Review Skill

Deferred from `handoff`.

- Review the current changes against the active work item, using `HANDOFF.md` as input.
- Record review results through `handoff` (event Record).
- Add to `handoff` when this skill exists:
  - Statuses: Reviewed with findings (waiting for fixes) and Reviewed (no findings; waiting for developer acceptance). Implemented then waits for review instead of acceptance.
  - Record cases: reviewed with findings → Reviewed with findings, list each finding; reviewed without findings → Reviewed; implemented again → remove resolved findings.
  - Next work item case: the new statuses get the reminder that the work item becomes Done only when committed and pushed.
  - Template section Review Findings: one line per finding, naming the file and the problem.
- Add to `work-done`: its preview shows the status and open threads when the status is not Reviewed, instead of not Implemented.
- Add to `setup`: the Statuses table in the `ISSUE-TRACKING.md` template gets a row per new status; existing `docs/ISSUE-TRACKING.md` files need these rows.
- Requires: Implement Skill.

## Git Context

Deferred from `handoff`.

- Decide how git context is used during implementation.
- `feature-plan` defines a work item as one pull request, while `work-done` pushes the current branch and creates no pull request. Decide where the branch and pull request per work item are created: in the Implement Skill or in `work-done`, not in `work-load`, which runs once per feature.
- `work-done` stages all uncommitted changes, including changes made before the active work item started.
- Requires: Implement Skill.
