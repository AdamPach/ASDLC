---
name: handoff
metadata:
  version: "0.1.1"
description: "Start, resume, or record the implementation state of the active feature in HANDOFF.md, the short-term memory between sessions. Use when implementation of a feature starts, at session start, and when a work item is implemented or accepted, or the developer asks for the next work item."
---

# Goal

Keep `HANDOFF.md` a short snapshot of where the active feature's implementation stands, so any session continues the work without the developer explaining it.

# Terminology

- **Handoff file:** `HANDOFF.md` in the root of the current checkout. Each checkout, including each worktree, has its own or none.
- **Active feature:** The feature the handoff file covers; at Start, the feature named in Details.
- **Implementation documents:** The active feature's implementation plan and work items.
- **Active work item:** The first work item in implementation-plan order whose status is not Done.

# Inputs

- **Event:** Required. Start, Resume, or Record; each Procedure section states when it applies. Not supplied → infer it from the turn; ask when unclear.
- **Details:** Optional. Facts for the event: the feature (Start), tests run, decisions, developer acceptance. Missing → take them from the turn.

# Procedure

1. Read the handoff file when it exists.
2. Follow the section for the event.

## Start (implementation of a feature begins)

1. Handoff file covers the same feature → follow Resume; stop.
2. Handoff file covers another feature:
   - That feature has work items not Done in its implementation documents → name them, ask whether to replace the handoff file; declined → stop.
   - All Done → continue silently.
3. Read the implementation documents.
4. Create the handoff file fresh from the template, replacing any existing one: link the implementation plan; set the active work item and its status.

## Resume (session start)

1. No handoff file → stop silently.
2. Read the implementation documents the handoff file links.
3. Compare the handoff file with the implementation documents:
   - The active work item's status differs from the implementation documents → ask the developer which is correct; write it to both.
   - The active work item is not the first work item in implementation-plan order whose status is not Done → set it to that work item.
   - A link does not resolve → ask the developer for the correct one; update the handoff file.
4. Report to the developer: active feature, active work item and its status, open threads, and the next step its status implies. Active work item None → report that all work items are Done.

## Record (a work item is implemented or accepted, or the developer asks for the next work item)

Apply the case that matches the active work item's new state, then update Unrecorded Decisions and Open Threads.

- Implemented and tested → Implemented. Update Tested.
- Accepted (only after the developer confirms) → Done. Clear Tested. Set the next active work item; none left → Active work item: None.
- Developer asks for the next work item while the active work item is not Done → ask whether to accept it; yes → apply Accepted; no → stop.

# Write Rules

Apply whenever the handoff file is written.

- Re-read the handoff file just before writing.
- Follow the template [HANDOFF.md](HANDOFF.md) in this skill's folder; leave no template prompts.
- **Snapshot:** Replace outdated content; never append history.
- **No copies:** Record only what the implementation documents and the repository do not show; link instead of restating. Remove a decision once it is written into the implementation documents.
- **Line cap:** 50 lines. Over it → shorten Tested and Unrecorded Decisions first; never remove links or the Active work item line.
- **Statuses:** Write each status change into the work item's Status field too.
  - Not started: waiting for implementation.
  - Implemented: implemented and tested; waiting for developer acceptance.
  - Done: the developer accepted it.
