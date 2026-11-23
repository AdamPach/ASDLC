# issue-tracking

Output: `docs/ISSUE-TRACKING.md`, from [../templates/ISSUE-TRACKING.md](../templates/ISSUE-TRACKING.md); replace its markers per Markers.

## Terminology

- **Stored documents:** Feature = `feature.md`; Implementation Plan = `implementation-plan.md`; Work Item = each `work-items/NN-<short-name>.md`. Each has one Document Mapping subsection.
- **Operations:** The subsections of the template's Operations section.
- **Suitable method:** One tool, with one authentication, that covers every Operation through its commands or its own raw API passthrough.
- **Closing keyword:** Commit text that changes an item's tracker state when the commit is pushed or merged.

## Procedure

1. Ask the developer to confirm the tracker and its location; the git remote is a hint, not the answer.
2. Research from official documentation:
   - The tracker's access methods. Installed tools and configured MCP servers are facts.
   - Per method: the invocation of each Operation; whether it is a suitable method.
   - Item types, relation types, content formats, and size limits.
   - The location's states: read them through a suitable method when it can; otherwise from documentation.
   - The reference syntax that links a commit in this repository to an item without a closing keyword, and any integration it requires.
3. Read the last 50 commit messages; collect their shared pattern, including where any item reference sits.
4. Run `interview`:
   - Topic: the project's issue tracking.
   - Perspective: access method, ASDLC item identification, document mapping, relations, statuses, commit linking, commit message format.
   - Context: the research; the commit message pattern.
   - Offer only suitable methods, each with the Operations it covers only through raw API.
   - Recommend the mapping and relations that use the tracker's native item types and relation types.
   - Referenced items: offer work item, feature, or both; recommend work item.
   - Commit message format: propose the collected pattern; no shared pattern → propose the default format. Never offer closing keywords.
5. Derive the Operations from the chosen method, the mapping, and the documentation.
6. Run the Verify invocation. Fails → report the failure; write nothing.
7. Write `docs/ISSUE-TRACKING.md` per Markers. Store no secrets; authentication stays each developer's own.

Default format:

```
<Summary line, imperative>

<1–3 sentences: what was implemented or changed>
```

## Markers

Replace each `[Marker]` in the template; leave none.

- `[Product]`: the tracker product.
- `[Location]`: the organization, repository or project, and area that hold ASDLC items.
- `[Identification]`: the label, tag, or item type that marks items ASDLC stores.
- `[Tool]`: the chosen suitable method and its minimum version.
- `[Prerequisites]`: installation, each developer's own authentication, required permissions, the integration commit linking requires.
- `[Verify]`: an invocation that proves access and the required permissions.
- `[Item]`: the document's item type. Implementation Plan may name the part of the feature item that holds it instead.
- `[Title]`: the title pattern; a work item's contains NN.
- `[Content]`: the field that holds the document, and its format conversion.
- `[Work item fields]`: the field, label, or tag that stores Type, and the one that stores Complexity.
- `[Plan relation]`: the relation type linking the feature item to its implementation plan item. Implementation Plan's Item is part of the feature item → `None`.
- `[Parent relation]`: the relation type, and which item is the work items' parent.
- `[Order relation]`: the relation type linking each work item to the next.
- `[Write state]`: the one tracker state Set Status writes for this ASDLC status.
- `[Read states]`: every tracker state that loads as this ASDLC status. Each tracker state appears in exactly one row.
- `[Reference syntax]`: the exact text that links a commit to one item, with an `<id>` placeholder. The tracker cannot link commits → `None`.
- `[Referenced items]`: work item, feature, or both. Reference syntax `None` → `None`.
- `[Commit template]`: the agreed message format, in a code block; each referenced item's reference syntax sits at its agreed position. Other values the committer supplies are `<name>` placeholders.
- `[Invocation]`: the exact command or tool call, in a code block. Values a calling skill supplies at run time are `<name>` placeholders. A Link Operation whose relation is `None` → `None`; remove its Returns and Notes lines.
- `[Returns]`: what the output contains. Load Feature: includes the implementation plan's ID when Plan relation is not `None`. List Work Items: the feature's work items in plan order, with ID and status. Find Features: ASDLC features with ID, title, and status.
- `[Notes]`: limits, conversions, or caveats; none → remove the line.
