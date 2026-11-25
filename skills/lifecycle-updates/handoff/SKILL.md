---
name: handoff
metadata:
  version: "0.4.0"
description: "Start, resume, or record the implementation state of the active feature in HANDOFF.md, the short-term memory between sessions; reads and writes the feature's documents and statuses in the issue tracker, or in the feature's request folder when the project has no issue tracker. Use when implementation of a feature starts, at session start, when AI stops implementing a work item before it is implemented and tested, when a work item is implemented or accepted, and when the developer asks for the next work item."
---

# Goal

Keep `HANDOFF.md` a short snapshot of where the active feature's implementation stands, so any session continues the work without the developer explaining it.

# Terminology

- **Handoff file:** `HANDOFF.md` in the root of the current checkout. Each checkout, including each worktree, has its own or none.
- **Tracking file:** `docs/ISSUE-TRACKING.md`.
- **Request folder:** `docs/features/NNN-short-request-name/`, holding a feature's `feature.md`, `implementation-plan.md`, and `work-items/NN-<short-name>.md`.
- **Source:** Where the feature's documents live: Tracker when the tracking file exists; otherwise Local.
- **Active feature:** The feature the handoff file covers; at Start, the feature named in Details.
- **Implementation documents:** The active feature's implementation plan and work items.
- **Active work item:** The first work item in implementation-plan order whose status is not Done.

# Inputs

- **Event:** Required. Start, Resume, or Record; each Procedure section states when it applies. Not supplied → infer it from the turn; ask when unclear.
- **Details:** Optional. Facts for the event: the feature's tracker link or ID, or its request folder (Start); where work stopped and why; tests run; developer acceptance. Missing → take them from the turn.

# Document Access

Applies whenever a feature, document, or status is found, loaded, written, or linked. Follow the part for the source.

## Tracker

- Access the issue tracker only through the tracking file's Operations.
- Find the feature: its tracker link or ID in Details.
- Find the implementation plan: from the feature per the tracking file's Document Mapping and Relations.
- Load the implementation documents: Load Implementation Plan; List Work Items for statuses and order; Load Work Item for the active work item only.
- Write a status: Set Status.
- Link an item: its tracker link; none → its ID.

## Local

- Find the feature: the request folder Details name by path or name. Not named or ambiguous → list the request folders that have an implementation plan and work items not all Done; the developer chooses.
- Find the implementation plan: `implementation-plan.md` in the request folder.
- Load the implementation documents: read the implementation plan for the work item order, each work item's Status line, and the active work item in full.
- Write a status: edit the work item's Status line.
- Link an item: its path relative to the project root.

# Procedure

1. Read the handoff file when it exists.
2. Follow the section for the event.

## Start (implementation of a feature begins)

1. Find the feature.
2. Handoff file covers the same feature → follow Resume; stop.
3. Handoff file covers another feature:
   - That feature has work items not Done → name them, ask whether to replace the handoff file; declined → stop.
   - All Done → continue silently.
4. Find the implementation plan.
5. Load the implementation documents.
6. Create the handoff file fresh from the template, replacing any existing one: link the feature, the implementation plan, and the active work item; set the active work item's status.

## Resume (session start)

1. No handoff file → stop silently.
2. Load the implementation documents the handoff file links. A link does not resolve → ask the developer for the correct one; update the handoff file.
3. Compare the handoff file with the implementation documents:
   - The active work item's status differs from the implementation documents → ask the developer which is correct; write it to both.
   - The active work item is not the first work item in implementation-plan order whose status is not Done → set it to that work item; load it.
4. Report to the developer: active feature, active work item and its status, progress, open threads, and the next step its status implies. Active work item None → report that all work items are Done.

## Record (the active work item's status changes, or the developer asks for the next work item)

Apply the case that matches the active work item's new state, then update Open Threads.

- AI stopped before it is implemented and tested → In progress. Update Progress; add an Open Thread for each reason; report the reasons to the developer.
- Implemented and tested → Implemented. Clear Progress. Update Tested.
- Accepted (only after the developer's finished work is committed and pushed) → Done. Clear Tested. Set the next active work item and its status; none left → Active work item: None.
- Developer asks for the next work item:
  - Active work item Not started → report it as the next work item; stop.
  - In progress or Implemented → tell the developer it becomes Done only when the finished work is committed and pushed; stop.
  - None → report that all work items are Done; stop.

# Write Rules

Apply whenever the handoff file is written.

- Re-read the handoff file just before writing.
- Follow the template [HANDOFF.md](HANDOFF.md) in this skill's folder; leave no template prompts.
- **Snapshot:** Replace outdated content; never append history.
- **Minimal:** Write only what the next session needs to continue the active work item, in the fewest lines.
- **No copies:** Record only what the implementation documents and the repository do not show; link instead of restating.
- **Statuses:** Write each status change to the work item too.
  - Not started: waiting for implementation.
  - In progress: AI stopped before the work item was implemented and tested; Progress states where, at least one Open Thread states why.
  - Implemented: implemented and tested; waiting for developer acceptance.
  - Done: the developer accepted it, and it is committed and pushed.
