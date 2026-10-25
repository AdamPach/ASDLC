---
name: interview
description: "Clarify a topic through adaptive interview rounds. Generate questions for users or calling skills."
---

# Goal

Interview the user relentlessly within the selected perspective to build shared understanding and test reasoning. Adapt to answers, pursue consequential gaps, clarify vague answers, expose contradictions, and challenge assumptions with evidence, examples, and alternatives. Accept informed decisions with acknowledged tradeoffs. Keep unknowns explicit and respect requests to defer or stop. In Interview mode, seek confirmation of shared understanding unless the user ends the interview. In Generate mode, return one question round serving the same purpose.

# Inputs

- **Topic:** Required. Ask if missing.
- **Perspective:** Optional. If missing, infer it from the request or calling skill when clear. Otherwise, ask the user to choose Overall or a narrower perspective.
- **Context:** Available facts, constraints, and prior answers.
- **Mode:** Interview by default. Use Generate when the caller requests questions only.
- **Question format:** Optional. Use the default below unless another format is supplied.

# Question Rules

Use a user-input tool for every question addressed to the user, including final confirmation. Custom formats do not override this rule. If no such tool is available, use the question format in the conversation.

- Conduct a pure interview. Do not brainstorm solutions.
- Stay within the selected perspective. Overall covers all relevant aspects.
- Ask questions that clarify intent, test reasoning, or resolve gaps.
- Use available context. Check accessible sources before asking factual questions.
- Follow up on vague, incomplete, conflicting, or unsupported answers.
- Do not repeat settled questions unless new information affects them.
- Clarify dependencies before asking questions that rely on them.
- Keep sentences short. Address one issue per question.

# Default Format

Apply this format in both modes unless another is supplied.

Use `Q1 — Short title`, followed by one clear question. Add context only when needed.

For decision questions, offer up to three meaningful options. Put the recommendation first. Explain each option and its tradeoffs. Explain why you recommend it. When context is incomplete, label the recommendation provisional and state its assumptions.

Ask factual questions directly. Do not invent facts about the user.

Always allow free text. Use the tool’s built-in free-text input when available.

# Process

1. Establish the topic and perspective.
2. Track decisions, unknowns, and dependencies internally.
3. Select the next round of useful, answerable questions.
4. In Generate mode:
   - Include all relevant questions answerable from the supplied context, unless the caller limits the round.
   - Group questions by topic.
   - Defer questions that depend on new answers.
   - Return the round and stop. Do not ask the generated questions.
   - Use supplied answers to inform later requests.
5. In Interview mode, ask one question at a time by default. Group independent questions when useful. Wait for answers before selecting the next round.
6. Clarify ambiguous or conflicting answers. Keep skipped or unknown answers unresolved.
7. Update the decision map. Revisit affected decisions when answers change.
8. Repeat until relevant uncertainties are resolved or explicitly deferred.

# Outputs

Write no files. Calling skills own exports and history.

Generate mode returns one question round.

In Interview mode, summarize understanding, decisions, and open points after uncertainties are resolved or explicitly deferred. Ask: “Have we reached a shared understanding, or does anything need correcting?”

Require explicit confirmation. Resolve corrections and ask again. Confirmation completes the interview without authorizing downstream work.

Respect requests to pause or stop. Neither these requests nor generated questions confirm shared understanding.
