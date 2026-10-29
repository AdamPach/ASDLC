---
name: feature-create
metadata:
  version: "0.1"
description: "Create one compact Markdown document from an already defined feature. Use to document its business purpose and behavior without clarifying the feature or choosing its technical implementation."
---

# Goal

Create one compact feature document from an already defined feature. Include the business information developers and AI need to understand how the feature works and make informed technical decisions. Preserve the agreed meaning and exclude information that does not support this purpose. Do not clarify the feature or choose its technical implementation.

# Terminology

- **Feature definition:** The existing description supplied in a document or available conversation, which provides the meaning the skill must preserve.
- **Supporting material:** Supplied or referenced information that supplements the feature definition, such as designs.
- **Business information:** What the feature does, who can use it, and the rules and conditions governing its behavior.
- **Feature document:** The compact Markdown output produced by this skill.

# Inputs

A feature definition describing its purpose, scope, and intended behavior, available as:

- **Document:** A supplied or referenced document, with relevant supporting material when available.
- **Conversation:** A definition established in the available conversation.

The definition must contain enough business detail to create the feature document without further clarification.

# Outputs

One compact Markdown feature document using the [feature template](templates/feature.md).

- **Content:** Replace prompts with information from the feature definition and relevant supporting material. Preserve necessary business details. Remove drafting prompts and instructions.
- **Style:** Use short, straightforward sentences in plain business language for nontechnical readers. Avoid technical language, unnecessary jargon, repetition, and contradictions. Use consistent terms and suitable prose, lists, or tables.
- **Sections:** Omit Appearance unless covered by the definition. Add clearly named sections only when necessary supplied information does not fit existing sections.

Save to `docs/features/<feature-name>.md` relative to the project root, using a lowercase, hyphenated feature name, unless the developer supplies another path.

# Workflow

1. Check the feature definition and relevant supporting material. If missing information or contradictions prevent accurate documentation, report the blockers and stop without creating or changing files. Do not resolve blockers or save a partial draft.
2. Determine the target path using Outputs. If a file already exists there, report the conflict and stop. Do not overwrite it or choose another filename.
3. Create and save the feature document using Outputs and the feature template. Do not require developer approval before saving.
4. Report the saved document’s location.

# Completion Criteria

- One feature document is saved at the target path.
- The document follows Outputs and the feature template, including the writing requirements.
- The document preserves the definition’s meaning without inventing information or choosing technical implementation.
- No drafting prompts or instructions remain in the document.
- The saved document’s location has been reported.
