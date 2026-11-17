---
name: docs-write
metadata:
  version: "0.1"
description: "Write and update project documentation under docs/ in a structure AI agents can navigate: files of at most 100 lines, one-level split folders with index.md, and docs/MAP.md. Use whenever documentation is created or a change to the project or a document makes existing documentation outdated."
---

# Goal

Write and maintain documentation that AI agents can read and navigate easily. Document only what the supplied sources support. Keep every file within the line cap, split oversized documentation into a one-level folder with an index, and keep `docs/MAP.md` and project links accurate.

# Terminology

- **Documentation:** All content about one subject that this skill manages, stored as single-file or split documentation.
- **Subject:** What a documentation describes.
- **Sources:** The material the caller supplies or identifies, including any change, plus project files and existing documentation relevant to the subject. The only basis for content.
- **Line cap:** 100 lines. Applies to every documentation file, index, area index, and the map.
- **Single-file documentation:** A documentation stored as `name.md`.
- **Split documentation:** A documentation stored as folder `name/` containing an index and content files, with no subfolders.
- **Index:** The `index.md` of a split documentation.
- **Content file:** Any file in a split documentation other than its index.
- **Map:** `docs/MAP.md`, the entry point listing every documentation or the area indexes that cover them.
- **Area:** A folder under `docs/` that groups related documentations. Its `index.md` is the **area index**.
- **Map entry:** A link, what the target covers, and when an agent should read it. Used in the map, indexes, and area indexes.

# Inputs

- **Subject:** Required. Take it from the caller's request or the sources.
- **Sources:** Required. Read the material the caller supplies or identifies, plus the project files and existing documentation relevant to the subject.
- **Target path:** Optional. When missing, find the subject's existing documentation through the map, area indexes, and indexes. When none exists, choose a descriptive path under `docs/`.

Write only content the sources support. Report content the sources cannot support. When no usable sources exist, stop and report it without creating or changing files.

# Outputs

Save all outputs without asking for approval.

- **Documentation:** Files created, updated, or deleted under `docs/` following Structure Rules and Writing Style.
- **Navigation:** The map, created when missing, and the affected indexes and area indexes, matching every path change.
- **Links:** Every project link to a changed path, updated.
- **Report:** Paths created, changed, moved, or deleted, and content the sources could not support.

# Structure Rules

Apply to every documentation file, index, area index, and the map.

- Keep every file within the line cap.
- Use single-file documentation while its content fits the line cap. Otherwise, convert it to split documentation, dividing content files by topics an agent would look up separately.
- When split documentation fits the line cap as one file, merge it back into single-file documentation.
- Write each index as a short overview of the subject followed by one map entry per content file. When the index cannot list every content file within the line cap, split the subject into sibling documentations.
- List one map entry per documentation or area index in the map. When the map would exceed the line cap, move related documentations into an area and replace their entries with one entry for the area index.
- List one map entry per documentation in each area index. When it would exceed the line cap, split the area into sibling areas. Keep areas once created.
- When a path is created, moved, merged, or removed, update the map, affected indexes and area indexes, and every project link to it.

# Writing Style

Apply to all documentation content, including indexes, area indexes, and the map.

- Write for AI agents first while keeping the text readable for developers.
- Describe only the current state. Remove outdated content; do not mark it as outdated or record its history.
- State each fact in one place. Link to it wherever else it is relevant.
- State the condition for every fact that holds only in some cases.
- Use one term for each concept.
- Add an example only when a precise description cannot convey the content on its own. Limit a code example to the smallest snippet that shows the pattern.
- Use short, direct sentences and descriptive headings. Use lists or tables when they make content easier to scan. Leave out filler.

# Workflow

1. Determine the subject, sources, and target path following Inputs.
2. Read the sources and the affected documentation. When no usable sources exist, stop and report it.
3. When the change removes the subject, delete its documentation and continue at step 5.
4. Write or update the content following Writing Style. Remove content the sources show is outdated.
5. Apply Structure Rules, including map, index, area index, and link updates.
6. Check Completion Criteria, fix failures, and report following Outputs.

# Completion Criteria

- Every documentation file, index, area index, and the map is within the line cap.
- Content is supported by the sources, follows Writing Style, and contains no outdated content.
- Split documentation has no subfolders. Each index and area index has one map entry per file or documentation it covers.
- The map covers every documentation directly or through an area index.
- No map entry, index entry, or project link points to a missing path.
- The report lists path changes and content the sources could not support.
