---
name: feature-write
metadata:
  version: "0.1"
description: "Create one compact feature document from a Ready feature definition produced by feature-discover or feature-discover-quick. Use to document the feature's business purpose and behavior for developers and AI without clarifying the feature or choosing its technical implementation."
disable-model-invocation: true
---

# Goal

Convert a Ready Feature Definition into one compact feature document. Include the business information developers and AI need to understand how the feature works and make informed technical decisions. Preserve the definition's meaning and leave out discovery records such as assumptions, open questions, and readiness. Do not clarify the feature or choose its technical implementation.

# Terminology

- **Feature Definition:** The `feature-definition.md` document produced by `feature-discover` or `feature-discover-quick`. It is the only source of the feature's meaning.
- **Ready:** The Feature Definition's Readiness Summary shows Status Ready and records the developer's explicit confirmation.
- **Request folder:** The `features/NNN-short-request-name/` folder that contains the Feature Definition.
- **Linked material:** Mockups, designs, or other references that the Feature Definition links.
- **Business information:** What the feature does, who can use it, and the rules and conditions governing its behavior.
- **Feature document:** The compact `feature.md` produced by this skill.

# Inputs

- **Feature Definition:** Required. Supplied as a path or identifiable from references or the request folder. Ask if missing or unclear. Do not accept a feature described only in the conversation or memory.
- **Linked material:** Optional. Read it only when needed to describe Appearance accurately.

Do not read interview documents (`questions-NNN.md`).

# Outputs

One compact Markdown feature document using the [feature template](templates/feature.md), saved as `feature.md` in the request folder. Replace an existing `feature.md` without asking.

- **Content:** Replace prompts with business information from the Feature Definition:
  - **Purpose and scope:** Request and Purpose; Context and Scope, including relevant current behavior.
  - **Users and permissions:** Users and access rules.
  - **Behavior:** Intended Behavior, Use Cases and Flows, and Entities and Fields.
  - **Appearance:** Appearance and Examples. Link linked material instead of copying it. Omit the section unless the definition covers appearance.
  - **Acceptance criteria:** Observable outcomes stated anywhere in the definition, written as checkable criteria. Add no outcome the definition does not state.
- **Exclusions:** Leave out Assumptions and Open Questions, Decision Rationale and References, the Readiness Summary, links to interview documents, and technical implementation choices.
- **Style:** Use short, straightforward sentences in plain business language for nontechnical readers. Avoid technical language, unnecessary jargon, repetition, and contradictions. Use consistent terms and suitable prose, lists, or tables.
- **Sections:** Add clearly named sections only when necessary business information does not fit existing sections.

# Workflow

1. Read the Feature Definition. If it is not Ready, report its status and stop without creating or changing files. Recommend finishing it with `feature-discover` or `feature-discover-quick` in Update mode.
2. Read linked material when Outputs requires it.
3. Create the feature document using Outputs and the feature template. If documenting the definition accurately would require guessing, report what is missing or contradictory and stop as in step 1. Otherwise, save it without asking for developer approval.
4. Report the saved location and recommend `feature-plan` next, in this session or a new one. If `implementation-plan.md` exists in the request folder, say it may be outdated and the developer should review it.

Do not edit the Feature Definition.

# Completion Criteria

- The Feature Definition was Ready.
- One feature document is saved as `feature.md` in the request folder.
- The document follows Outputs and the feature template, including the writing requirements.
- The document preserves the definition's meaning without inventing information or choosing technical implementation.
- No drafting prompts, instructions, or excluded content remain in the document.
- The Feature Definition is unchanged.
- The saved location and the next step have been reported, including the outdated-plan notice when it applies.
