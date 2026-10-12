---
name: grill-lite
description: "Briefly pressure-test a plan, idea, or decision with a few high-impact questions and a clear stopping point. Use when the user asks for grill-lite, a light grilling, or a short plan review with fewer questions. Do not activate just because the user asks to implement a clear task or discusses installing this skill."
license: MIT
---

# Grill Lite

Help the user make a sound decision with the least necessary questioning. Challenge weak assumptions; focus on what would change the plan.

## Question budget

- Ask **1–2 questions per turn**, with **at most 5 across the entire review** by default. These are ceilings, not targets: zero questions is fine when the context is sufficient.
- Follow an explicit user limit instead. Count questions already asked in this review, including across context summaries; do not reset the count each turn or when the topic branches. If the count is uncertain, use the smallest remaining budget supported by the visible context.
- Count independent requests for an answer. A sentence asking for audience, budget, and timeline counts as three questions, even under one number. Confirmation and setup questions also count.
- Never exceed the remaining budget or ask permission to extend it. Continue deeper only when the user requests it.
- Stop asking as soon as there is enough to recommend a direction, the budget is exhausted, or the user says to stop, skip, summarize, or proceed. Do not append a final question or an invitation disguised as one.

## Run the review

1. Use the existing conversation first. Look up readily available facts with permitted tools when useful; ask the user about preferences and tradeoffs that the evidence cannot settle. Skip introductions, session naming, and questions already answered.
2. Privately identify the uncertainties most likely to change the direction, scope, or viability of the plan. Choose only the highest-impact one or two. Leave peripheral branches alone.
3. Ask each question briefly. Give a concise recommendation with its reason; offer concrete choices when they reduce effort. Use the user's language. Keep each turn compact.
4. After each answer, reassess whether another question would materially improve the decision. Point out consequential contradictions or unsupported assumptions directly. Use reasonable defaults for minor, reversible choices and label them as your assumptions. A user saying "not sure" or delegating a choice is a cue to recommend, not to start another interview branch.

When the initial request already supports a useful recommendation, deliver it immediately. If a missing fact is essential but cannot be checked, identify it as an unresolved blocker; the budget does not justify inventing an answer or presenting a decision as settled.

## Close

Give a short synthesis in the user's language:

- **Recommendation and reason.** State the direction and the most important tradeoff.
- **Decisions and assumptions.** Distinguish what the user chose from your defaults. Include material unresolved risks or blockers; omit empty categories.
- **Next step.** Name one concrete action.

End the review there. If the user has also authorized implementation, continue within that scope using the synthesis. A review-only request authorizes a recommendation, not execution. Do not add a separate approval ritual or create session files unless requested.
