---
name: interview
description: "Clarify a topic through adaptive interview rounds. Generate questions for users or calling skills."
---

# Goal

Generate questions that help the user or calling skill clarify a topic from a selected perspective. Use answers to build shared understanding, expose assumptions, and resolve relevant uncertainties. Guide the interview through an internal decision map. Each round should clarify open points and reveal which questions to ask next. Adapt to answers rather than follow a fixed questionnaire. In Interview mode, continue until the user confirms the summary of decisions and remaining open points. In Generate mode, return one question round for the caller to use.

# Input

- **Topic:** Required. Ask if missing.
- **Perspective:** Optional. If missing, first ask the user to choose Overall or enter a narrower perspective.
- **Context:** Available facts, constraints, and prior answers.
- **Mode:** Interview by default. Use Generate when the caller requests questions only.
- **Question format:** Optional. Use the default below unless another format is supplied.

# Question Rules

Use the Ask User tool or an equivalent user-input tool for every question asked of the user. This includes opening questions, topic and perspective selection, follow-ups, and final confirmation. Custom question formats do not override this requirement. Only when no such tool is available, use the same structured question format in the conversation.

- Stay within the selected perspective. Overall covers all relevant aspects.
- Resolve uncertainty, test assumptions, or clarify decisions.
- Use available context. Do not repeat answered questions.
- Check accessible sources before asking factual questions.
- Ask only questions whose prerequisites are settled.
- Keep sentences short. Ask one clear question at a time within each round.

# Default Format

Use `Q1 — Short title`, followed by a brief question description.

Offer up to three meaningful choices. Put a justified recommendation first. Do not invent choices or recommendations.

Always allow free text. Use the tool's built-in free-text input when available.

# Process

1. Establish the topic and perspective.
2. Track decisions, unknowns, and dependencies internally.
3. Select the next round of useful, answerable questions.
4. In Generate mode, return the round to the caller and stop.
5. In Interview mode, ask the round and wait for answers.
6. Clarify ambiguous or conflicting answers. Keep skipped or unknown answers unresolved.
7. Update the decision map. Revisit affected decisions when answers change.
8. Repeat until relevant uncertainties are resolved or explicitly deferred.

# Output and Completion

Write no files. Calling skills own exports and stored history. Generate mode returns questions. Use supplied answers to generate later rounds.  In Interview mode, summarize the agreed understanding, decisions, and open points. Explicitly ask: “Have we reached a shared understanding, or does anything need correcting?” Wait for explicit user approval before completing the interview. Silence or ambiguous replies do not count as approval. If corrections are needed, resolve them, update the summary, and ask again. Confirmation completes the interview. It does not authorize downstream work.
