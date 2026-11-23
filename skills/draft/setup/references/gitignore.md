# gitignore

Output: `.gitignore` in the repository root.

## Terminology

- **ASDLC entries:** One root-anchored entry per document the Document Map in `ASDLC.md` marks as not committed, at its stated location.
- **Finding:** A proposed change to `.gitignore` with its reason, in one category:
  - Missing ignores: files the project's stack or current untracked files show should be ignored.
  - Tracked but should not be: committed files that should be ignored.
  - Over-ignoring: entries that ignore files that must be shared, including every other document the Document Map lists.
  - Broken entries: duplicates, entries cancelled by a later negation, entries that match nothing.

## Procedure

1. Read the Document Map in `ASDLC.md`; collect the ASDLC entries.
2. Inspect the project's stack, untracked files, tracked files, and existing `.gitignore`; collect findings. Never propose ASDLC entries; they are always written.
3. Run `interview`:
   - Topic: the project's `.gitignore`.
   - Perspective: what the developer wants ignored; the findings.
   - Context: ASDLC entries, findings, existing `.gitignore`.
   - Order: one proposals question per category with findings; then ask what else should be ignored. An answer raises new findings → ask them as proposals questions.
4. Write `.gitignore`:
   - A `# ASDLC` block holds exactly the ASDLC entries; missing → create it at the top.
   - Group new accepted entries under one short comment per purpose.
   - Keep existing lines in place; change only accepted fixes and removals.
5. Report also lists each accepted entry that matches tracked files, with `git rm --cached <path>` per path. Never run it.

Proposals question format:

```
Question: <category> — <n> proposed changes
Multi-select options, one per finding; above the tool's option limit → split over several questions:
  label: <entry or path>
  description: <add | remove | fix>; <reason>
```
