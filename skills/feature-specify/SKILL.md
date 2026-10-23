---
name: feature-specify
description: "Test"
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

## Interview Documents

Create `questions-NNN.md` when clarification is needed, one file per interview round, numbered sequentially from `001` within the request folder. Preserve every question and keep its answer alongside it. The Requester may answer in chat or directly in the file; keep the document updated. Distinguish proposals, confirmed answers, and unresolved points. Use `Awaiting answer` until answered. Keep skipped or unknown answers unresolved. Incorporate confirmed outcomes into the Feature Definition and retain completed interview documents as history.

## Document Templates

Use the [Feature Definition](templates/feature-definition.md) and [Interview Round](templates/interview-round.md) templates for document structure. Interview topic headings may vary by round. Remove authoring comments and replace placeholders in generated documents.

# Workflow

# Clarification Guide

## Question Generation

Use the `questions` skill in Generate mode for one round at a time. Supply the Product Request as the topic and limit the perspective to business needs and product behavior: how it should work, not how to implement it. Include available context, prior answers, confirmed decisions, assumptions, and open points. Supply the formats below. This skill owns the saved documents.

Include all relevant unanswered questions that can be asked from the current context. Do not impose a question limit or restrict a round to one topic. Check available sources first. Defer questions whose prerequisites depend on new answers. Use each round's answers to generate the next round; revisit answered questions only when new information affects them.

## Question Format

Ask one clear question at a time. Keep sentences short. Add brief context and impact when useful. Allow custom answers and never invent choices to fit a format. Put justified recommendations first and explain them briefly.

- [Single select](question-types/single-select.md): choose one alternative.
- [Multi select](question-types/multi-select.md): choose several applicable options.
- [Entity modeling](question-types/entity-modeling.md): review proposed entity information, relationships, and business rules. Avoid database design.
- [Open text](question-types/open-text.md): answer freely when choices or a table do not fit.

## Round Organization

Group questions by logical topic using `##` headings. Topics may mix question types. Use `### Q[N] — [Short title]` for each question. Number questions consecutively across the round, starting at `Q1`. Repeat topic sections and question blocks as needed.

# When the Feature is Ready