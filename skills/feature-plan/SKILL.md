---
name: feature-plan
metadata:
  version: "0.1"
description: "Create an implementation plan and ordered work items from a feature document. Use to agree with the developer how to implement the feature in the existing codebase and split it into small, reviewable increments that keep the product working."
disable-model-invocation: true
---

# Goal

Create an implementation plan and an ordered set of work items from a feature document. Interview the developer about how to implement the feature in the existing codebase. Start from the developer's view, fill gaps, and explain options when the developer does not know. Split the feature into small work items. Each work item must leave the product working and be small enough for an AI agent to implement and the developer to review in one sitting. Keep the developer in control of and responsible for implementation decisions. Do not change business requirements.

# Terminology

- **Feature document:** The Markdown document created by `feature-write`. It holds the feature's business information. It is the source of business requirements, and this skill does not change it.
- **Developer:** The person running the skill. The developer makes the implementation decisions and is responsible for the product.
- **Implementation decision:** An agreed choice about how to implement the feature, such as where it fits in the codebase, which libraries it uses, or how data and interfaces change.
- **Implementation plan:** The document that holds the feature-wide implementation decisions and the split.
- **Work item:** One small increment that an AI agent implements and the developer reviews as one pull request, described in its own document. Work items are numbered WI 1 to WI n.
- **Split:** The ordered list of work items for the feature.
- **Vertical slice:** A work item that adds user-observable behavior end to end, across every layer it needs.
- **Enabler:** A work item with no new user-observable behavior that prepares the code for later work items.
- **Working product:** The project builds and starts. Existing behavior and existing automated tests still work. The acceptance criteria of all completed work items pass.
- **Acceptance criteria:** Observable outcomes the developer checks manually to verify a work item.
- **Complexity:** A work item's estimated implementation demand, combining difficulty and amount of change: Small, Medium, Large, or Extra-large. It helps the developer choose a model. Every work item must still pass Size in Split Rules.

# Inputs

- **Feature document:** Required. Created by `feature-write`, usually at `docs/features/<feature-name>.md`. Ask if missing.
- **Codebase:** Required. The project the feature will be implemented in.
- **Context:** Optional. Developer notes, constraints, or prior technical decisions.

# Outputs

Save to `docs/features/<feature-name>/`, using the feature document's name:

- `implementation-plan.md`: Implementation decisions and the split, using the [implementation plan template](templates/implementation-plan.md).
- `work-items/NN-<short-name>.md`: One work item per split entry, numbered from `01` in split order, using the [work item template](templates/work-item.md).

Link each work item to the implementation plan and the feature document. Work items may link to earlier work items. Write each work item so an AI agent can implement it in a new session from the work item and its linked documents.

# Workflow

1. Read the feature document and explore the codebase for the modules, patterns, libraries, and data the feature affects. If the output folder already contains an implementation plan or work items, report it and stop.
2. Run the implementation interview.
3. Propose the split using Split Rules.
4. Present the implementation plan, including the split, and ask for approval to save. On change requests, revise and ask again. Return to the interview when a change affects an implementation decision. Save only after approval.
5. Write all work items and present them together. Ask for approval to save. On change requests, revise and ask again. Save only after approval.
6. Report the saved locations, and recommend implementing WI 1 in a new session.

If the feature document has a business gap or contradiction at any step, report it and stop.

# Implementation Interview

Use `interview` in Interview mode, in one session. Supply the feature as the topic and implementation as the perspective: architecture and integration, libraries and technology choices, and data and interfaces. Supply the feature document and codebase findings as context.

Supply this question format, keeping the other `interview` rules:

- Ask how the developer imagines each decision first. Include relevant codebase facts, but no options or recommendation.
- Fill gaps and challenge answers against the codebase.
- Offer up to three explained options, with a recommendation, only when the developer does not know.

The confirmed session provides the implementation decisions for the implementation plan.

# Split Rules

Use judgment to cut the feature, and explain the reasoning for each cut.

- **Slice type:** Make each work item a vertical slice. Use an enabler only when it leaves a working product, has its own acceptance criteria, and would otherwise make a vertical slice fail Size. State why it is needed, and place it directly before the first work item that needs it.
- **Size:** Each work item covers one primary behavior or enabler goal, has its own acceptance criteria, fits in one pull request, and can be reviewed in one sitting, roughly under an hour. Split any work item that fails a check.
- **Order:** Each work item naturally continues from those before it, usually starting with the simplest complete path. Implementing WI 1 to WI n in order must cause no dependency problems.
- **Working product:** Every work item leaves a working product and may expose its behavior when completed. Do not plan feature flags, hidden entry points, or similar mechanisms.
- **Coverage:** Assign every behavior and business rule in the feature document to a work item, and every implementation decision to the work items that apply it. Plan nothing the feature document does not require.

Present each work item with its number, title, type, complexity, goal, covered behavior, and reasoning. If the split seems too long for one feature, say why and let the developer decide whether to continue or return to `feature-discover` or `feature-discover-quick`.

# Completion Criteria

- The developer confirmed the implementation interview session.
- The implementation plan and work items are saved after explicit approval.
- The split meets every Split Rule.
- Each work item links to the implementation plan and feature document and includes acceptance criteria.
- No template prompts remain.
- The saved locations and the next step have been reported.
