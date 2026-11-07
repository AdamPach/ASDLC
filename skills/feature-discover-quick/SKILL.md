---
name: feature-discover-quick
metadata:
  version: "0.1"
description: "Create or update a feature definition through a chat interview with the developer and confirm it is ready for feature-write."
disable-model-invocation: true
---

# Goal

Create or update a feature definition through one chat interview with the developer. Clarify the whole feature's purpose, scope, and product behavior, and leave technical choices for later. Keep answers the developer cannot give as open questions for the PO.

# Terminology

- **Product Request** - A proposal for a new product capability or a change to an existing one. It may be vague or incomplete.
- **Product Owner (PO)** - The person who makes product decisions for the Product Request. The PO does not take part in the chat; the developer relays the PO's input.
- **Developer** - The person who runs this skill, answers questions in chat, relays PO input, and confirms the Feature Definition.
- **Feature** - A product capability being introduced or changed by the Product Request.
- **Feature Definition** - The `feature-definition.md` document produced or updated by this skill. It captures the currently understood requirements and behavior and may remain incomplete while open questions remain.
- **Open question** - An unresolved product decision that needs the PO, recorded under Open Questions in the Feature Definition.
- **Interview summary** - The chat summary of decisions, assumptions, open questions, and the readiness result that the developer confirms before this skill writes the Feature Definition.
- **Mode** - Whether the current run creates a new Feature Definition or updates an existing one. The mode concerns the definition document, regardless of whether the request introduces a new capability or changes an existing one.

# Inputs

Determine the mode from the developer's intent and available context. Use Create for a new Feature Definition and Update to revise an existing one, including after the PO answers open questions. Update accepts definitions created by `feature-discover`. If the mode or target definition is unclear, ask a focused clarification question.

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

**Optional Context:**
- New or revised information, such as PO answers to open questions or changes from the developer. The interview asks for what is missing.
- Relevant product documentation, code, or examples of current behavior.
- UI mockups, screenshots, sketches, or user flows illustrating the intended appearance or behavior.
- Prior decisions, constraints, or dependencies relevant to the update.

Ignore interview documents (`questions-NNN.md`) in the request folder. Do not read, edit, or create them.

# Output Documents

Create or update one Feature Definition per Product Request. It captures the feature's purpose, scope, intended behavior, and, where relevant, appearance. It summarizes relevant context, distinguishes confirmed requirements from assumptions, and lists open questions.

## Location and Naming

Store software documentation under `docs/` at the target project's root. Use `docs/features/NNN-short-request-name/feature-definition.md` for each Product Request. Number request folders sequentially from `001` and use lowercase names with hyphens. Reuse the existing request folder in Update mode.

## Feature Definition

Maintain the Feature Definition as the current understanding and agreed outcome of the Product Request. Include relevant existing behavior and distinguish confirmed requirements, assumptions, and open questions.

Always include Request and Purpose, Context and Scope, Intended Behavior, and Assumptions and Open Questions. Mark unknowns explicitly. Place the Readiness Summary at the end.

Add optional sections when they help explain the feature. Capture all relevant behavior even when an optional section is omitted. Define each requirement once and link related details. Remove optional labels and template prompts from the finished document.

Replace superseded decisions; note significant tradeoffs under Decision Rationale and References. Do not add links to interview documents; leave existing ones unchanged.

## Document Template

Use the [Feature Definition](templates/feature-definition.md) template for document structure. Remove authoring comments and replace placeholders in generated documents. Ignore template prompts that refer to interview documents.

# Workflow

1. Read the Product Request and available context. Determine the mode and target folder using Inputs and Output Documents. In Update mode, read the existing Feature Definition.
2. Interview the developer about the whole feature using the Clarification Guide. Record answers the developer cannot give as open questions. Write nothing during the interview unless the developer asks to save. If they ask, write the current understanding, mark the Readiness Summary Not ready with the interview in progress, and continue. If the developer stops the interview, end the run without writing unless they ask to save.
3. When the interview ends, review the understanding to be written against all six areas under When the Feature is Ready. If an Unresolved area can be clarified with the developer, continue the interview. If an Update run changed nothing, list the open questions still awaiting the PO and end the run without writing.
4. Present the interview summary and ask the developer whether it is correct. Apply corrections and ask again. Silence or ambiguous replies do not count as confirmation.
5. Write the Feature Definition from the confirmed interview summary and update the Readiness Summary.
6. End the run:
   - **Review passes:** Follow Confirmation and Handoff.
   - **Open questions remain:** List the open questions the developer should take to the PO. Tell the developer to rerun this skill in Update mode with the answers.

# Clarification Guide

Use the `interview` skill in Interview mode, with one session for the whole run. Supply the Product Request as the topic and limit the perspective to business needs and product behavior: how it should work, not how to implement it. Include available context and, in Update mode, the Feature Definition's confirmed decisions, assumptions, and open questions. Use interview's default question format. This skill owns the Feature Definition and readiness assessment.

- In Update mode, start with new information and open questions. Revisit settled decisions only when new information affects them.
- When the developer cannot answer, record an open question and move on.
- Resolve conflicts with existing decisions in the interview. Record a conflict as an open question when it needs a PO decision.
- End the interview when interview would present its session summary. Replace that summary and its confirmation with the interview summary (Workflow step 4).

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
- **Next step:** What is needed to proceed or resume, such as the open questions the developer should take to the PO. When ready, state the handoff to `feature-write`.

If requirements change after confirmation, mark the definition Not ready. Require a new review and confirmation of the updated definition. Wording-only edits that preserve requirements do not invalidate confirmation.

## Confirmation and Handoff

When the review passes, present the assessment in chat and ask the developer to explicitly confirm the complete Feature Definition. Silence or ambiguous replies do not count as confirmation.

If the developer requests corrections, apply those the developer can decide, including behavior the developer states the PO already agreed to. Then repeat the review and ask for confirmation again. If a correction needs a new PO decision, record it as an open question, mark the definition Not ready, and end the run as in Workflow step 6.

The feature is ready only when the review passes and the developer confirms the complete definition. Record that confirmation and mark the Readiness Summary Ready. Then recommend using `feature-write`, in this session or a new one, to convert the clarified material into one compact feature file. Provide the path to the definition for that handoff.
