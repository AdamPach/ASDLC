---
name: feature-discover
metadata:
  version: "0.1"
description: "Create or update a feature definition from a product request. Use to clarify scope, product behavior, and business rules through interview documents answered by the product owner, resolve gaps and contradictions, and confirm readiness for feature-write. Leave technical implementation choices for later."
disable-model-invocation: true
---

# Goal

Turn a Product Request into a Feature Definition that defines its product behavior completely and consistently, and that the developer confirms is ready for `feature-write`. Reach it through interview rounds answered by the PO, keeping assumptions and open points visible until they are resolved.

# Terminology

- **Product Request** - A proposal for a new product capability or a change to an existing one. It may be vague or incomplete.
- **Product Owner (PO)** - The person who makes product decisions for the Product Request and answers clarification questions in interview documents.
- **Developer** - The person who runs this skill, shares interview documents with the PO, and confirms the final Feature Definition in chat.
- **Interview round** - One set of clarification questions for the PO, saved as one `questions-NNN.md` interview document.
- **Feature** - A product capability being introduced or changed by the product request.
- **Feature Definition** - The main document produced or updated by this skill. It captures the currently understood requirements and behavior and may remain incomplete while relevant questions are unresolved.
- **Mode** - Whether the current run creates a new Feature Definition or updates an existing one. The mode concerns the definition document, regardless of whether the request introduces a new capability or changes an existing one.

# Inputs

Determine the working mode from the user's intent and available context. Use Create when a new Feature Definition is requested and Update when an existing Feature Definition is to be revised. Use Update also to continue clarification after the PO answers a round. Update accepts definitions created by `feature-discover-quick`. If the intended mode or target definition is unclear, ask a focused clarification question.

## Create

**Required Input:**
- A description of the Product Request, which may be vague, incomplete, or unstructured.

**Optional Context:**
- Relevant product context, including intended users, goals, known constraints, and prior decisions.
- Existing documentation, code, or examples of current product behavior.
- UI mockups, screenshots, sketches, or user flows illustrating the intended appearance or behavior.
- Supporting documents or examples from the PO or developer that help clarify the request.

## Update

**Required Input:**
- The existing Feature Definition, provided directly or identifiable from references, available context, or existing files.
- New or revised information to incorporate, such as answers in interview documents or changes and clarifications from the developer.

**Optional Context:**
- Existing interview documents, including answered and unresolved questions. Definitions created by `feature-discover-quick` may have none.
- Relevant product documentation, code, or examples of current behavior.
- UI mockups, screenshots, sketches, or user flows illustrating the intended appearance or behavior.
- Prior decisions, constraints, or dependencies relevant to the update.
- Additional supporting material from the PO or developer that helps clarify the requested changes.

# Output Documents

Based on the available inputs, create or update the Feature Definition and any supporting interview documents. Together, these documents serve as a decision map for the feature, capturing its purpose, scope, intended behavior, and, where relevant, appearance. They summarize relevant context and confirmed product decisions, distinguish assumptions from confirmed requirements, and identify open questions and decisions that still need to be resolved.

## Folder Structure

```text
docs/
└── features/
    ├── 001-short-request-name/
    │   ├── feature-definition.md
    │   ├── questions-001.md
    │   └── questions-002.md
    └── 002-another-request-name/
        └── feature-definition.md
```

## Location and Naming

Store software documentation under `docs/` at the target project's root. Use `docs/features/NNN-short-request-name/` for each Product Request. Number request folders sequentially from `001` and use lowercase names with hyphens. Reuse the existing request folder in Update mode.

## Feature Definition

Maintain `feature-definition.md` as the current understanding and agreed outcome of the Product Request. Include relevant existing behavior and distinguish confirmed requirements, assumptions, and unresolved points. Keep the definition understandable without reading the interview documents.

Always include Request and Purpose, Context and Scope, Intended Behavior, and Assumptions and Open Questions. Mark unknowns explicitly. Place the Readiness Summary at the end.

Add optional sections when they help explain the feature. Capture all relevant behavior even when an optional section is omitted. Define each requirement once and link related details. Remove optional labels and template prompts from the finished document.

## Interview Documents

Create `questions-NNN.md` when clarification is needed, one file per interview round, numbered sequentially from `001` within the request folder. Preserve every question. The PO answers directly in the file, alongside each question. Distinguish proposals, confirmed answers, and unresolved points. Use `Awaiting answer` until answered. Mark a question repeated in a later round `Carried to Round NNN`. Keep skipped or unknown answers unresolved. Incorporate confirmed outcomes into the Feature Definition and retain completed interview documents as history.

## Document Templates

Use the [Feature Definition](templates/feature-definition.md) and [Interview Round](templates/interview-round.md) templates for document structure. Interview topic headings may vary by round. Remove authoring comments and replace placeholders in generated documents.

# Workflow

1. Read the Product Request and available context. Determine the mode and target folder using the Inputs and Output Documents sections.
2. In Create mode, save an initial Feature Definition. Mark assumptions and unknowns explicitly. In Update mode, read the existing definition and interview documents. Record answers from the latest round and incorporate other new information. If the latest round has no new answers and the developer supplied no other new information, report that the round awaits answers and end the run without changes. If no rounds exist yet, continue.
3. Check answers and new information against each other and existing decisions. Incorporate confirmed outcomes into the definition. Keep each conflict unresolved; in the next round, explain it and ask the PO whether to change the earlier decision. Retain superseded decisions in the interview history.
4. Review all six areas under When the Feature is Ready and update the Readiness Summary.
5. End the run in one of these ways:
   - **Review passes:** Follow Confirmation and Handoff.
   - **Clarification can progress:** Generate one round using the Clarification Guide. Repeat the previous round's unanswered questions, linking each to its original. Save the round. Tell the developer which file the PO should answer and to rerun this skill in Update mode afterwards.
   - **Nothing can progress:** Use the Readiness Summary to explain why the feature is not ready and what is needed to resume.

Ask product questions only in interview documents. Ask the developer in chat only to clarify the mode or target definition and for final confirmation. Do not ask for approval of intermediate drafts. Ask skipped or unknown questions again only when new information is available.

# Clarification Guide

## Question Generation

Use the `interview` skill in Generate mode for one round at a time. Supply the Product Request as the topic and limit the perspective to business needs and product behavior: how it should work, not how to implement it. Include available context, prior answers, confirmed decisions, assumptions, and open points. Supply the formats below. This skill owns the saved documents and readiness assessment.

Include all relevant unanswered questions that can be asked from the current context. Do not impose a question limit or restrict a round to one topic. Check available sources first. Defer questions whose prerequisites depend on new answers. Use each round's answers to generate the next round; revisit answered questions only when new information affects them.

## Question Format

Each question should address one clear decision. Keep sentences short. Add brief context and impact when useful. Allow custom answers and never invent choices to fit a format. Put justified recommendations first and explain them briefly.

- [Single select](question-types/single-select.md): choose one alternative.
- [Multi select](question-types/multi-select.md): choose several applicable options.
- [Entity modeling](question-types/entity-modeling.md): review proposed entity information, relationships, and business rules. Avoid database design.
- [Open text](question-types/open-text.md): answer freely when choices or a table do not fit.

## Round Organization

Group questions by logical topic using `##` headings. Topics may mix question types. Insert complete question-type blocks beneath each topic. Each block supplies its question heading and answer field. Number questions consecutively across the round, starting at `Q1`. Repeat topic sections and question blocks as needed.

# When the Feature is Ready

## Readiness Review

Review the complete Feature Definition, including behavior not covered by interview questions. Assess these six areas within the agreed scope:

- **Purpose and scope:** Intended users, desired outcome, included behavior, and exclusions.
- **Flows:** Triggers, normal paths, alternative paths, failures, and recovery.
- **Business rules and information:** Relevant entities, fields, validation, relationships, and state changes.
- **Access:** Who can access the feature and what they can see or do.
- **Experience and constraints:** Relevant appearance, interactions, accessibility, and product limits.
- **Verifiable outcomes:** Observable behavior that distinguishes correct from incorrect results.

Assign each area a status and briefly explain the assessment:

- **Resolved:** Relevant product behavior is defined and consistent. No missing detail, ambiguity, or unconfirmed assumption affects that behavior.
- **Not applicable:** The area does not apply to this feature. State why.
- **Unresolved:** Relevant details are missing, ambiguous, contradictory, or based on unconfirmed assumptions. Identify what must be clarified.

The review passes only when every area is Resolved or Not applicable. Any Unresolved area prevents readiness and feeds further clarification. Leave technical implementation choices for later.

## Readiness Summary

Keep a short Readiness Summary as the final section of the Feature Definition. Update it whenever the definition, review result, or confirmation changes. Record:

- **Status:** Ready or Not ready.
- **Reason:** Brief review result. If not ready, identify unresolved areas or missing confirmation. Link existing details instead of repeating them.
- **Confirmation:** Whether the developer explicitly confirmed the current definition in chat.
- **Next step:** What is needed to proceed or resume, such as the interview document the PO should answer. When ready, state the handoff to `feature-write`.

If requirements change after confirmation, mark the definition Not ready. Require a new review and confirmation of the updated definition. Wording-only edits that preserve requirements do not invalidate confirmation.

## Confirmation and Handoff

When the review passes, present the assessment in chat and ask the developer to explicitly confirm the complete Feature Definition. Documents-only clarification does not apply to this confirmation. Silence or ambiguous replies do not count as confirmation.

If the developer requests corrections, apply those the developer can decide, including behavior the developer states the PO already agreed to. Then repeat the review and ask for confirmation again. If a correction needs a new PO decision, save it in a new round and end the run as in Workflow step 5.

The feature is ready only when the review passes and the developer confirms the complete definition. Record that confirmation and mark the Readiness Summary Ready. Then recommend using `feature-write`, in this session or a new one, to convert the clarified material into one compact feature file. Provide the path to the definition and its supporting documents for that handoff.
