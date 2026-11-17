---
name: handoff-write
metadata:
  version: "0.1"
description: "Create, update, or reset HANDOFF.md, the short-term memory of the active feature's current work. Use at the end of every turn in which work on the active feature progressed or a review produced results, and when work on a different feature starts."
---

# Goal

Keep `HANDOFF.md` a short snapshot of the active feature's current work, so any new session can continue or review the work without the developer explaining it. Record only what the repository does not show yet: work item progress, what was tested, unrecorded decisions, the next step, and review findings. Keep work item statuses synchronized with the work item documents and the file within its line cap.

# Terminology

- **Handoff file:** `HANDOFF.md` in the root of the current checkout. Each checkout, including each worktree, has its own handoff file or none.
- **Active feature:** The one feature the handoff file covers.
- **Feature documents:** The active feature's feature definition, feature document, implementation plan, and work items, whichever exist.
- **Phase:** The active feature's lifecycle stage: discover, write, plan, or implement.
- **Active work item:** The work item with status In progress or In review. If none, the next work item with status Not started.
- **Base commit:** The commit checked out when the active work item moved to In progress.
- **Unrecorded decision:** A decision or deviation from the feature documents agreed during the work and not yet written into them.
- **Implementer section:** The handoff file's part that records the active feature's progress.
- **Review section:** The handoff file's part that records review findings for the active work item.
- **Review turn:** A turn spent reviewing the active work item's changes.
- **Reset:** Replacing the handoff file with a new one for a different active feature.

# Inputs

- **Turn's work:** Required. What the current turn changed, decided, tested, or reviewed for the active feature, taken from the conversation and the repository.
- **Handoff file:** Optional. Read it when it exists. When it does not exist, create it.
- **Feature documents:** Required. Read the documents the handoff file links. When the handoff file does not exist, identify the active feature from the turn's work and read its documents in `features/`.
- **Repository state:** The current commit and uncommitted changes.
- **Reset request:** Optional. The developer's request to reset the handoff file.

# Outputs

- **Handoff file:** Created, updated, or reset, following [templates/handoff.md](templates/handoff.md) and Handoff Rules.
- **Work item statuses:** The `Status:` field of each work item whose status changed.
- **Questions to the developer:** Only for conflicts between the handoff file and the repository, and for resets. Otherwise, update silently.

# Workflow

1. If the turn has no work on any feature and no reset request, stop without changes.
2. Read the handoff file just before writing, so changes another session made are kept.
3. If the handoff file exists, compare it with the feature documents and the repository: work item statuses, linked files, and recorded commits. If they differ, list the differences, ask the developer which version is correct, and apply the answer to both before continuing.
4. Reset when the developer requested it. When the turn's work belongs to a different feature than the active feature, ask whether to reset and name the active feature's work items that are not Done. If the developer declines, stop without changes.
5. When resetting, or when the handoff file does not exist, create the handoff file from the template for the feature of the turn's work.
6. In a review turn, update the review section and the active work item's status. In any other turn, update only the implementer section. Follow Handoff Rules.
7. Write each changed work item status into that work item's `Status:` field.

# Handoff Rules

- **Snapshot:** Replace outdated content instead of appending history.
- **No copies:** Record only what the feature documents and the repository do not show. Link to documents instead of restating them. Remove an unrecorded decision once it is written into the feature documents.
- **Line cap:** Keep the handoff file at 50 lines or fewer. When it would exceed the cap, shorten finished and older information first, and keep links, the active work item, and review findings.
- **Statuses:** Use only Not started, In progress, In review, and Done.
  - Set In progress when implementation of the work item starts, and record the base commit.
  - Set In review when the implementer considers the work item complete and tested.
  - When a review finds issues, set In progress and list each finding in the review section. Remove a finding when the implementer resolves it.
  - Set Done only after the developer confirms the work item is accepted.
- **Review section:** Clear it when the active work item changes.

# Completion Criteria

- The handoff file reflects the turn's work, or Workflow stopped without changes.
- The turn changed only the section it owns, except a review turn changing the active work item's status.
- Every work item's `Status:` field matches its status in the handoff file.
- The handoff file has 50 lines or fewer, follows the template, and contains no template prompts.
- The developer confirmed every conflict resolution and every reset that was not requested.
