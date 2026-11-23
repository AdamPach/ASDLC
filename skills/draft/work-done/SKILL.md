---
name: work-done
metadata:
  version: "0.1.0"
description: "Commit and push the developer's finished work in the project's commit format, and record the active work item as Done. Only the developer invokes it, via /work-done, when the work is done."
disable-model-invocation: true
---

# Goal

Turn finished work into one pushed commit that also records the active work item as Done.

# Procedure

## 1. Draft

1. Read all uncommitted changes, untracked files included.
2. Choose the format:
   - `docs/ISSUE-TRACKING.md` has a Commits section whose Reference is not None, and `HANDOFF.md` has an active work item that is not None → its Commit template, with each Referenced item's ID in the Reference syntax. Take each ID from the items `HANDOFF.md` links and their parent items; not found → ask the developer.
   - Otherwise → the default format, with no reference.
3. Write the commit message in the chosen format; describe only the changes.

Default format:

```
<Summary line, imperative>

<1–3 sentences: what was implemented or changed>
```

## 2. Approve

1. Ask the developer to approve with the user-input tool; its preview shows the message and the files to commit. Approval confirms the work is done.
   - Approved → continue.
   - Message or file changes requested → apply them; ask again.

## 3. Record

1. `HANDOFF.md` exists and its active work item is not None → invoke `handoff` with event Record and detail: the active work item is accepted, and the finished work is being committed.

## 4. Commit and Push

1. Stage all changes, untracked files included, except `HANDOFF.md` and files the developer excluded.
2. Commit with the approved message exactly as shown in the preview.
3. Push the current branch; no upstream → push it to `origin` under the same name and set it as upstream.
