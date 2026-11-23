---
name: feature-push
metadata:
  version: "0.0.1"
description: "Push a planned feature's documents (feature, implementation plan, work items) to the issue tracker per docs/ISSUE-TRACKING.md, link them, and delete the local request folder, so the tracker becomes their only source of truth. Only the developer invokes it, via /feature-push, before implementation starts."
disable-model-invocation: true
---

# Goal

Move a planned feature's documents into the issue tracker, so the tracker becomes their only source of truth.

# Terminology

- **Request folder:** The `docs/features/NNN-short-request-name/` folder that holds the pushed documents.
- **Pushed documents:** In the request folder: `feature.md`, `implementation-plan.md`, and each `work-items/NN-<short-name>.md`.
- **Tracking file:** `docs/ISSUE-TRACKING.md`. Its Document Mapping, Relations, Statuses, and Operations define every tracker action; access the tracker only through its Operations.
- **Tracker link:** The link to a created item that its Create Operation returns; no link returned → its ID.

# Procedure

## 1. Check

Any check fails → report it, stop.

1. Read the pushed documents; ask for the request folder when unclear.
2. Confirm `feature.md`, `implementation-plan.md`, and at least one work item exist.
3. Confirm every work item's Status is Not started.
4. Confirm the tracking file exists and contains no `[Marker]`; run its Verify invocation.
5. Run Find Features; confirm no feature has the title the Feature mapping gives this feature.

## 2. Approve

1. Ask for approval with the user-input tool; its preview lists each item to create (document, title, item type, relations) and the request folder to delete.
   - Approved → Push.
   - Not approved → stop.

## 3. Push

Convert each document per its Document Mapping. Any Operation fails → report the items created so far with their tracker links, stop.

1. Create Feature.
2. Create Implementation Plan; rewrite its feature link to a tracker link.
3. Per work item, in plan order: Create Work Item, then Set Status to Not started. In its content, rewrite links to tracker links; remove the Status line, and the Type and Complexity lines when Work item fields store them.
4. Update Implementation Plan with the content from step 2, its work item links also rewritten to tracker links.
5. For each relation the Relations section defines, link every pair of created items it applies to.

## 4. Delete and Report

1. Delete the request folder. Never commit.
2. Report each created item with its tracker link, and that the deletion is uncommitted; recommend implementing work item 01 in a new session.
