---
name: discuss
description: "Discuss a plan, idea, or decision, one short question at a time, with suggested options, a recommendation, room for your own ideas, and a default limit of five discussion questions. Use for direct requests such as discuss, discuss一下, 讨论, 讨论一下, 聊聊, 探讨一下, grill, grill一下, grill me, grill-lite, or grill_lite, and similar requests to talk through a plan. Do not activate for quoted or negated phrases, skill installation/renaming/explanation, or a clear implementation-only request. Respect an explicit request for a different skill."
license: MIT
---

# Discuss

Help the user think through a plan and make a sound decision with the least necessary questioning. Challenge weak assumptions; focus on what would change the plan.

## Question budget

- Ask **one discussion question at a time**, with **at most 5 across the entire review** by default. After asking, wait for the user's answer before choosing or asking the next question. Zero discussion questions is fine when the context is sufficient.
- Follow an explicit user limit instead. Count discussion questions already asked in this review, including across context summaries; do not reset the count each turn or when the topic branches. If the count is uncertain, use the smallest remaining budget supported by the visible context. An explicit cap on all questions or turns also includes the closing execution confirmation.
- Count independent requests for an answer. Audience, budget, and timeline are three questions, even in one sentence; pick only one to ask now. Setup questions and confirmation of plan details also count. Alternative answers to the same decision are options, not additional questions. The single execution choice in **Close** is separate from the default discussion budget; it cannot carry additional planning questions.
- Never exceed the remaining budget or ask permission to extend it. Continue deeper only when the user requests it.
- Stop discussion questions as soon as there is enough to recommend a direction, the budget is exhausted, or the user says to stop, skip, summarize, or proceed. Give the synthesis, then follow **Close** to decide whether to ask for execution or finish there.

## Run the review

1. Use the existing conversation and evidence to identify the goal, relevant constraints, and confirmed decisions. Look up missing facts with permitted tools only when they could change the current question, options, or recommendation. Skip introductions, session naming, and questions already answered.
2. Choose the unresolved tradeoff whose plausible answers would most change the direction, scope, viability, or next action. For minor, reversible details already implied by earlier answers, use reasonable defaults and label them as assumptions. If no consequential choice needs the user's judgment, give the synthesis now.
3. Ground the recommendation in those facts, constraints, and the user's priorities. When recommending a change to existing responsibilities or scope, use the brief recommendation reason to state its benefit and main cost. Existing arrangements can be challenged, especially when the user explicitly wants to revisit them.
4. Use the question format below. Then stop and wait. Do not preview later questions, simulate the user's answer, or treat the recommended option as selected. Accept a letter, a combination or modification of the options, or an entirely new idea. Use the user's actual answer to guide the review; do not force it into a listed choice or ask for a letter confirmation.
5. After each answer, carry forward the user's decisions and reassess the remaining tradeoffs. Point out consequential contradictions or unsupported assumptions directly. Do not spend another question just to confirm a minor default. A user saying "not sure" or delegating a choice is a cue to recommend, not to start another interview branch.

When the initial request already supports a useful recommendation, deliver it immediately. If a missing fact is essential but cannot be checked, identify it as an unresolved blocker; the budget does not justify inventing an answer or presenting a decision as settled.

## Question format

Every question uses the same compact layout:

```text
🍢 {number}/{limit}: {one short question}

- A. {recommended option} (Recommended)
- B. {alternative option}
- C. {alternative option, omit if unnecessary}

🔥 {one short reason for the recommendation}

Reply with a letter, or share your own idea.
```

- Always provide **2–3 concrete options** for the same decision. Put the recommendation first as **A**, clearly mark it, and bold that option when Markdown is supported. Do not replace choices with an open-ended prompt or invent facts to construct them.
- Keep the question to one short sentence, each option to a short phrase, and the recommendation reason to one short sentence. Skip long introductions and analysis paragraphs. Ask only the displayed question in that turn.
- Keep the emoji fixed: **🍢** for the question and **🔥** for the recommendation reason. Do not rotate symbols or add decorative emoji. Show the running question count using the current review's total limit.
- Show the short free-text invitation on every question: **回复字母，或直接说你的想法。** in Chinese, **Reply with a letter, or share your own idea.** in English. It is an answer instruction, not an additional question. Options are suggestions, not an exhaustive list; the recommendation is advice, not a constraint on the user's choice.
- Use the user's language throughout, including the recommendation marker: **（推荐）** in Chinese, **(Recommended)** in English.

## Close

Give a short synthesis in the user's language:

- **Recommendation and reason.** State the direction and the most important tradeoff.
- **Decisions and assumptions.** Distinguish what the user chose from your defaults. Include material unresolved risks or blockers; omit empty categories.
- **Next step.** Name one concrete action.

A discussion request alone does not authorize execution. After the synthesis, follow the user's latest direction when choosing the ending:

- **Already authorized:** carry out the agreed next action within the authorized scope, without asking again.
- **Ready to act, not yet authorized:** if the next action is concrete, within the agent's capabilities, and has no material blocker, ask one execution question about that action and its scope. Use the compact format above with **Start confirmation** / **开始确认** in place of `{number}/{limit}`. Offer **A. Start (Recommended)**, **B. Adjust the plan (describe the changes)**, and **C. Stop here**, localized to the user's language. Include the brief 🔥 reason and free-text invitation, then wait. Do not label this `6/5` or use it to ask more planning questions.
- **Finish with the synthesis:** do this when the user requested advice only, explicitly said not to execute or to stop, a material blocker remains, the agent cannot perform the next action, or the execution question would exceed an explicit all-inclusive cap.

A Start selection or a clear affirmative reply to the execution question authorizes only the action and scope just summarized; proceed without another start confirmation. If the user chooses adjustment, use their corrections and keep the discussion count; do not infer execution permission or restart the questionnaire. A revised proposal may need its own execution choice. If the user stops, end there. Do not create session files unless requested.
