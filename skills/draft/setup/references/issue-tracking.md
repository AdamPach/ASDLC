# issue-tracking

Output: `docs/ISSUE-TRACKING.md`, from [../templates/ISSUE-TRACKING.md](../templates/ISSUE-TRACKING.md); replace its markers per Markers.

## Terminology

- **Stored documents:** Feature = `feature.md`; Implementation Plan = `implementation-plan.md`; Work Item = each `work-items/NN-<short-name>.md`. Each has one Document Mapping subsection.
- **Operations:** The subsections of the template's Operations section.
- **Suitable method:** One tool, with one authentication, that covers every Operation through its commands or its own raw API passthrough.

## Procedure

1. Ask the developer to confirm the tracker and its location; the git remote is a hint, not the answer.
2. Research from official documentation:
   - The tracker's access methods. Installed tools and configured MCP servers are facts.
   - Per method: the invocation of each Operation; whether it is a suitable method.
   - Item types, relation types, content formats, and size limits.
   - The location's states: read them through a suitable method when it can; otherwise from documentation.
3. Run `interview`:
   - Topic: the project's issue tracking.
   - Perspective: access method, ASDLC item identification, document mapping, relations, statuses.
   - Context: the research.
   - Offer only suitable methods, each with the Operations it covers only through raw API.
   - Recommend the mapping and relations that use the tracker's native item types and relation types.
4. Derive the Operations from the chosen method, the mapping, and the documentation.
5. Run the Verify invocation.
6. Write `docs/ISSUE-TRACKING.md` per Markers. Store no secrets; authentication stays each developer's own.

## Markers

Replace each `[Marker]` in the template; leave none.

- `[Product]`: the tracker product.
- `[Location]`: the organization, repository or project, and area that hold ASDLC items.
- `[Identification]`: the label, tag, or item type that marks items ASDLC stores.
- `[Tool]`: the chosen suitable method and its minimum version.
- `[Prerequisites]`: installation, each developer's own authentication, required permissions.
- `[Verify]`: an invocation that proves access and the required permissions.
- `[Item]`: the document's item type. Implementation Plan may name the part of the feature item that holds it instead.
- `[Title]`: the title pattern; a work item's contains NN.
- `[Content]`: the field that holds the document, and its format conversion.
- `[Work item fields]`: the field, label, or tag that stores Type, and the one that stores Complexity.
- `[Parent relation]`: the relation type, and which item is the work items' parent.
- `[Order relation]`: the relation type linking each work item to the next.
- `[Write state]`: the one tracker state Set Status writes for this ASDLC status.
- `[Read states]`: every tracker state that loads as this ASDLC status. Each tracker state appears in exactly one row.
- `[Invocation]`: the exact command or tool call, in a code block. Values a calling skill supplies at run time are `<name>` placeholders.
- `[Returns]`: what the output contains. List Work Items: the feature's work items in plan order, with ID and status. Find Features: ASDLC features with ID, title, and status.
- `[Notes]`: limits, conversions, or caveats; none → remove the line.
