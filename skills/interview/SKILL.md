---
name: interview
description: "Clarify a topic through adaptive interview sessions. Generate question batches for users or calling skills."
---

# Goal

Interview the user relentlessly within the selected perspective to build shared understanding and test reasoning. Adapt to answers, seek useful missing knowledge, clarify vague answers, expose contradictions, and challenge assumptions with evidence, examples, and alternatives. Accept informed decisions with acknowledged tradeoffs.

# Terminology

- **Topic:** The subject being clarified.
- **Perspective:** The aspects of the topic the questions focus on.
- **Decision map:** The conceptual structure of a topic’s possible decisions, questions, and dependencies. Each answer adds knowledge about it.
- **Session:** A defined scope for establishing and confirming shared understanding.
- **Batch:** All relevant questions that can be generated from current knowledge without depending on new answers.
- **Shared understanding:** The user-confirmed understanding reached within a session, including points they explicitly deferred or said they do not know.

# Inputs

- **Topic:** Required. Ask if missing.
- **Perspective:** Optional. If missing, infer it from the request or calling skill when clear. Otherwise, ask the user to choose Overall or a narrower perspective.
- **Context:** Available facts, constraints, assumptions, prior answers, and decisions.
- **Sessions:** Use one session for the conversation unless the user or calling skill defines separate scopes.
- **Mode:** Interview by default. Use Generate when the caller requests questions only.
- **Question format:** Optional. Use the default below unless another format is supplied.

# Question Rules

Use a user-input tool whenever asking the user a question, including session confirmation. Custom formats do not override this rule. If unavailable, ask in the conversation using the question format.

- Offer alternatives to clarify decisions; do not expand into solution brainstorming.
- Focus on the selected perspective. Overall covers all relevant aspects. Ask necessary questions outside it without otherwise expanding the scope.
- Ask only for useful knowledge missing from available context.
- Check accessible sources before asking factual questions.
- Revisit settled questions only when new information affects them.
- Keep sentences short. Address one issue per question.

# Default Format

Apply this format in both modes unless another is supplied.

Use `Q1 — Short title`, followed by one clear question. Add context or examples only when needed to understand the question.

For decision questions, offer up to three meaningful options. Explain each option and its tradeoffs. When justified, put a recommendation first and briefly explain why. If context is incomplete, label the recommendation provisional and state its assumptions.

Ask factual questions directly. Do not invent facts about the user.

Always allow free text. Use the tool’s built-in free-text input when available.

# Process

1. Establish the topic, perspective, and session scope. Reuse relevant knowledge from earlier sessions.
2. Review context and prior answers across the whole session scope, including aspects not yet discussed. Distinguish confirmed answers, assumptions, and gaps.
3. In Generate mode, return one batch of all currently relevant questions that do not depend on new answers, grouped by topic. Stop without asking them.
4. In Interview mode:
   - If every relevant gap is resolved, explicitly deferred by the user, or the user says they do not know, follow Outputs.
   - Otherwise, choose the next useful question. Resolve prerequisites and contradictions before dependent questions. Ask exactly one question and wait for the answer.
   - Check the answer against earlier knowledge. Clarify vague, incomplete, conflicting, or unsupported answers; revisit affected decisions across sessions and repeat from step 2.

# Outputs

Write no files. Calling skills own exports and history.

Generate mode returns one batch.

In Interview mode, summarize the session’s understanding, decisions, assumptions, and open points. Keep deferred and unknown points explicit. Ask: “Have we reached a shared understanding, or does anything need correcting?”

Require explicit confirmation for each session. If corrected, repeat Process from step 2 before requesting confirmation again. Confirmation completes the session without authorizing downstream work.

Respect requests to pause or stop. Neither these requests nor generated questions confirm shared understanding.
