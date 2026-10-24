---
name: feature-specify
description: "Create or update a feature definition from a product request. Use to clarify scope, product behavior, and business rules through questions, resolve gaps and contradictions, and confirm readiness for feature-create. Leave technical implementation choices for later."
disable-model-invocation: true
---

# Goal

Create or update a feature definition and its supporting documents within a dedicated folder. Use the user's description and available context to clarify the request's purpose, scope, and intended behavior, asking questions where needed. Focus clarification on product behavior and rules rather than technical implementation choices. The main document should capture the current understanding and confirmed requirements, clearly distinguishing assumptions and unresolved points. Record each clarification round in a separate interview document.

# Terminology

- **Product Request** - A proposal for a new product capability or a change to an existing one. It may be vague or incomplete.
- **Requester** - the person who submits the product request
- **Feature** - A product capability being introduced or changed by the product request.
- **Feature Definition** - The main document produced or updated by this skill. It captures the currently understood requirements and behavior and may remain incomplete while relevant questions are unresolved.
- **Mode** - Whether the current run creates a new Feature Definition or updates an existing one. The mode concerns the definition document, regardless of whether the request introduces a new capability or changes an existing one.

# Inputs

Determine the working mode from the user's intent and available context. Use Create when a new Feature Definition is requested and Update when an existing Feature Definition is to be revised. If the intended mode or target definition is unclear, ask a focused clarification question.

## Create

**Required Input:**
- A description of the Product Request, which may be vague, incomplete, or unstructured.

**Optional Context:**
- Relevant product context, including intended users, goals, known constraints, and prior decisions.
- Existing documentation, code, or examples of current product behavior.
- UI mockups, screenshots, sketches, or user flows illustrating the intended appearance or behavior.
- Supporting documents or examples from the Requester that help clarify the request.

## Update

**Required Input:**
- The existing Feature Definition, provided directly or identifiable from references, available context, or existing files.
- New or revised information to incorporate, such as requested changes, clarifications, or answers to previously identified questions.

**Optional Context:**
- Existing question documents, including answered and unresolved questions.
- Relevant product documentation, code, or examples of current behavior.
- UI mockups, screenshots, sketches, or user flows illustrating the intended appearance or behavior.
- Prior decisions, constraints, or dependencies relevant to the update.
- Additional supporting material from the Requester that helps clarify the requested changes.

# Output Documents

Based on the available inputs, create or update the Feature Definition and any supporting question documents. Together, these documents serve as a decision map for the feature, capturing its purpose, scope, intended behavior, and, where relevant, appearance. They summarize relevant context and confirmed product decisions, distinguish assumptions from confirmed requirements, and identify open questions and decisions that still need to be resolved.

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

Create `questions-NNN.md` when clarification is needed, one file per interview round, numbered sequentially from `001` within the request folder. Preserve every question and keep its answer alongside it. The Requester may answer in chat or directly in the file; keep the document updated. Distinguish proposals, confirmed answers, and unresolved points. Use `Awaiting answer` until answered. Keep skipped or unknown answers unresolved. Incorporate confirmed outcomes into the Feature Definition and retain completed interview documents as history.

## Document Templates

Use the [Feature Definition](templates/feature-definition.md) and [Interview Round](templates/interview-round.md) templates for document structure. Interview topic headings may vary by round. Remove authoring comments and replace placeholders in generated documents.

# Workflow

1. Read the Product Request and available context. Determine the mode and target folder using the Inputs and Output Documents sections.
2. In Create mode, save an initial Feature Definition before asking clarification questions. Mark assumptions and unknowns explicitly. In Update mode, read the existing definition and interview documents. Check new information for conflicts with existing decisions. Incorporate confirmed changes and flag conflicts for clarification.
3. Review the definition using the six areas under When the Feature is Ready. If clarification is needed, generate one round using the Clarification Guide. Save the questions in an interview document. Present them to the Requester and wait for answers.
4. Record the answers. Check them against each other and existing decisions. If answers conflict, explain the conflict and ask whether the Requester intends to change an earlier decision. Incorporate confirmed outcomes into the definition. Retain superseded decisions in the interview history.
5. Review all six areas again after each update. Update the Readiness Summary at the end of the definition. If answerable gaps remain, continue directly to the next needed clarification round. Do not require approval of intermediate drafts. When the review passes, follow the confirmation and handoff steps below.

If a required answer is unavailable, keep it unresolved and continue with other answerable questions. Revisit it when new information is available or the Requester is ready to answer. If no further clarification can progress, stop the rounds. Use the Readiness Summary to explain why the feature is not ready and what is needed to resume.

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
- **Confirmation:** Whether the Requester explicitly confirmed the current definition.
- **Next step:** What is needed to proceed or resume clarification. When ready, state the handoff to `feature-create`.

If requirements change after confirmation, mark the definition Not ready. Require a new review and confirmation of the updated definition. Wording-only edits that preserve requirements do not invalidate confirmation.

## Confirmation and Handoff

When the review passes, present the assessment and ask the Requester to explicitly confirm the complete Feature Definition. If corrections are requested, update the definition, repeat the review, and ask for confirmation again. Silence or ambiguous replies do not count as confirmation.

The feature is ready only when the review passes and the Requester confirms the complete definition. Record that confirmation and mark the Readiness Summary Ready. Then recommend using `feature-create` in a new session to convert the clarified material into one compact feature file. Provide the path to the definition and its supporting documents for that handoff.
