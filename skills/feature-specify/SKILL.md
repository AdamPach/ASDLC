---
name: feature-specify
description: "Test"
---

# Goal

Create or update a feature definition and its supporting documents within a dedicated folder. Use the user's description and available context to clarify the request's purpose, scope, and intended behavior, asking questions where needed. Focus clarification on product behavior and rules rather than technical implementation choices. The main document should capture the current understanding and confirmed requirements, clearly distinguishing assumptions and unresolved points. Where useful, provide separate question documents to support further clarification.

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

# Workflow

# Clarification Guide

# When the Feature is Ready
