---
name: handoff
metadata:
  version: "0.1.0"
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

- **Event:** Required. Start, Resume, or Record; see Procedure. Not supplied → infer it from the turn; ask when unclear.
- **Details:** Optional. Facts for the event: the feature (Start), tests run, decisions, developer acceptance. Missing → take them from the turn.

# Procedure

1. Read the handoff file when it exists.
2. Read the reference for the event and follow it:
   - Start (implementation of a feature begins) → `references/start.md`
   - Resume (session start) → `references/resume.md`
   - Record (a work item is implemented or accepted, or the developer asks for the next work item) → `references/record.md`

# Write Rules

Apply whenever the handoff file is written.

- Re-read the handoff file just before writing.
- Follow [templates/handoff.md](templates/handoff.md); leave no template prompts.
- **Snapshot:** Replace outdated content; never append history.
- **No copies:** Record only what the implementation documents and the repository do not show; link instead of restating. Remove a decision once it is written into the implementation documents.
- **Line cap:** 50 lines. Over it → shorten Tested and Unrecorded Decisions first; never remove links or the Active work item line.
- **Statuses:** Write each status change into the work item's Status field too.
  - Not started: waiting for implementation.
  - Implemented: implemented and tested; waiting for developer acceptance.
  - Done: the developer accepted it.
