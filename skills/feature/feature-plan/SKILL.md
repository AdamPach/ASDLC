---
name: feature-plan
metadata:
  version: "0.0.3"
description: "Turn a feature document into an implementation plan and ordered work items through a developer interview grounded in code facts."
disable-model-invocation: true
---

# Goal

Turn a feature document into an implementation plan and ordered work items. The developer makes every implementation decision; business requirements never change.

# Terminology

- **Feature document:** `feature.md` in the request folder: the feature's business description (purpose and scope, users and permissions, behavior, appearance, acceptance criteria); the source of business requirements.
- **Request folder:** The `docs/features/NNN-short-request-name/` folder that holds the feature document.
- **Code facts:** Current codebase state relevant to the feature or a decision: existing implementations of similar problems and what is used now, each with its file path.
- **Implementation decision:** An agreed choice of how to implement the feature: where it fits in the codebase, which libraries it uses, how data and interfaces change.
- **Work item:** One increment an AI agent implements and the developer reviews as one pull request; numbered from 01 in split order.
- **Split:** The ordered list of work items.
- **Working product:** The project builds and starts; existing behavior and automated tests still work; the acceptance criteria of all completed work items pass.
- **Acceptance criteria:** Observable outcomes the developer checks manually to verify a work item.

# Procedure

Every step: business gap or contradiction in the feature document, or a decision that would change a business requirement → report it, stop.

## 1. Start

1. Read the feature document. Ask for its path when unclear.
2. `implementation-plan.md` or `work-items/` exists in the request folder → report it, stop.

## 2. Explore

1. Collect the code facts the feature touches: modules, patterns, libraries, data model, interfaces, tests.

## 3. Interview

1. Run `interview` in Interview mode, one session:
   - Topic: the feature.
   - Perspective: architecture and integration, libraries and technology, data and interfaces.
   - Context: the feature document and code facts.
   - Question format: the decision question format below, for decision questions.
2. Before each decision question, collect the code facts it needs.
   - No relevant code facts → collect research facts instead: patterns that fit the project's stack; search the web when the choice depends on current libraries, versions, or practices.
3. Put a recommended option first only when the facts support it.
4. Use the confirmed session's decisions as the implementation decisions.

Decision question format:

```
Question text:
  Code facts:
  - <fact> (<path>)
  Research facts:
  - <fact> (<URL> | known pattern)
  <one question>
Options (2–3):
  label: <approach> [(Recommended)]
  description: <how it works>; <tradeoff>; <reason, when recommended>
  preview: <file layout or code sketch>, when it helps
Free text: the tool's built-in input
```

Show Code facts, or Research facts when step 2 found no relevant code facts.

## 4. Split

1. Split the feature into work items per the split rules; record the reasoning for each work item boundary in the plan's Split section.
2. Two or more splits meet the split rules and differ in scope or order → ask the developer in the decision question format.
3. The split seems too long for one feature → explain why; the developer chooses to continue or stop.

Split rules:
- **Vertical slice:** Default type. Adds user-observable behavior end to end, across every layer it needs.
- **Enabler:** Adds no user-observable behavior; prepares code for later work items. Use only when it leaves a working product, has its own acceptance criteria, and a vertical slice would otherwise fail Size. Place it directly before the first work item that needs it; state why it is needed.
- **Size:** One primary behavior or enabler goal, its own acceptance criteria, one pull request, reviewable in one sitting (roughly under an hour). Fails a check → split it.
- **Order:** Each work item continues from the previous ones, usually starting with the simplest complete path. Implementing work items in number order causes no dependency problems.
- **Working product:** Every work item leaves a working product and may expose its behavior. No feature flags, hidden entry points, or similar mechanisms.
- **Coverage:** Assign every behavior, business rule, permission, appearance requirement, and feature acceptance criterion in the feature document to a work item, and every implementation decision to the work items that apply it. Plan nothing the feature document does not require; changes to existing code count when a required behavior needs them.
- **Complexity:** Rate each work item Small, Medium, or Large by implementation demand (difficulty and amount of change) to guide model choice.

## 5. Write

1. Write to the request folder:
   - `implementation-plan.md` from [templates/implementation-plan.md](templates/implementation-plan.md).
   - One `work-items/NN-<short-name>.md` per work item from [templates/work-item.md](templates/work-item.md). Write each so an AI agent can implement it in a new session from it and its linked documents.
2. Ask one review question: the preview shows the implementation plan; the question text lists the work item paths.
   - Like it → Report.
   - Wording change → edit, ask again.
   - Decision or split change → return to Interview or Split; rewrite the affected files; ask again.

## 6. Report

1. Report the saved paths; recommend pushing the feature document, implementation plan, and work items to the issue tracker before implementation.
