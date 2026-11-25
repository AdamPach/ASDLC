---
name: work-done
metadata:
  version: "0.3.1"
description: "Commit and push the developer's finished work in the project's commit format, and record the active work item as Done. Only the developer invokes it, via /work-done, when the work is done."
disable-model-invocation: true
---

# Goal

Turn finished work into one pushed commit that also records the active work item as Done.

# Procedure

## 1. Draft

1. Read all uncommitted changes, untracked files included.
2. Choose the format:
   - `docs/ISSUE-TRACKING.md` has a Commits section → its Commit template:
     - Reference is not None, and `HANDOFF.md` has an active work item that is not None → each Referenced item's ID in the Reference syntax. Take each ID from the items `HANDOFF.md` links and their parent items; not found → ask the developer.
     - Otherwise → leave out the references.
   - No Commits section → the default format, with no reference.
3. Write the commit message in the chosen format; describe only the changes.

Default format:

```
<Summary line, imperative>

<1–3 sentences: what was implemented or changed>
```

## 2. Approve

1. Ask the developer to approve with the user-input tool. Approval confirms the work is done. Its preview shows:
   - the message and the files to commit;
   - `HANDOFF.md` has an active work item that is not None → that this work item becomes Done; its status is not Implemented → also its status and open threads.
2. Handle the answer:
   - Approved → continue.
   - Message or file changes requested → apply them; ask again.

## 3. Commit

1. Stage all changes, untracked files included, except `HANDOFF.md` and files the developer excluded.
2. Commit with the approved message exactly as shown in the preview.

## 4. Push

1. Push the current branch; no upstream → push it to `origin` under the same name and set it as upstream.
2. Push fails → report the failure; stop.

## 5. Record

1. `HANDOFF.md` exists and its active work item is not None → invoke `handoff` with event Record and detail: the active work item is accepted, and its work is committed and pushed.
