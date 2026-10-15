---
name: discuss
description: "Discuss a plan, idea, or decision, one short question at a time, with options, a recommendation, and room for your own ideas. Ask up to five questions per round, with optional deeper rounds. Use for direct requests such as discuss, discuss一下, 讨论, 讨论一下, 聊聊, 探讨一下, grill, grill一下, grill me, grill-lite, or grill_lite, and similar requests to talk through a plan. Do not activate for quoted or negated phrases, skill installation/renaming/explanation, or a clear implementation-only request. Respect an explicit request for a different skill."
license: MIT
---

# Discuss

Help the user think through a plan and make a sound decision with the least necessary questioning. Challenge weak assumptions; focus on what would change the plan.

## Rounds and question budget

- Ask **one discussion question at a time**, with **at most 5 per round** by default. Wait for the answer before choosing the next question. Five is a ceiling, not a target or a promised total; zero questions is fine when the context is sufficient.
- Track the round's discussion count internally across turns, topic branches, and context summaries. Reset it only when the user chooses or requests a deeper round after a synthesis. Carry forward all earlier decisions and constraints. There is no fixed limit on the number of rounds, but each new round requires the user's choice; reaching five never starts another automatically.
- Follow explicit user limits and their scope. A limit across the whole review persists across rounds; a cap on all questions or turns includes closing choices too. Do not offer another round when it would exceed that cap, or solicit an increase. The user can explicitly revise the limit. If the count is uncertain, use the smallest remaining budget supported by the visible context.
- Count independent requests for an answer. Audience, budget, and timeline are three questions, even in one sentence; pick one. Setup questions and confirmation of plan details also count. Alternative answers to the same decision are options, not additional questions. The single next-step choice in **Close a round** is separate from the default discussion budget and cannot carry extra planning questions.
- Close the round as soon as there is enough to recommend a direction, the round's budget is exhausted, or the user says to stop, skip, summarize, or proceed. Briefly explain the natural stopping point, then give the synthesis. Do not fill unused slots or imply that questions are missing.

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
🍢 Question {number}: {one short question}

- A. {recommended option} (Recommended)
- B. {alternative option}
- C. {alternative option, omit if unnecessary}

🔥 {one short reason for the recommendation}

Reply with a letter, or share your own idea.
```

- Always provide **2–3 concrete options** for the same decision. Put the recommendation first as **A**, clearly mark it, and bold that option when Markdown is supported. Do not replace choices with an open-ended prompt or invent facts to construct them.
- Keep the question to one short sentence, each option to a short phrase, and the recommendation reason to one short sentence. Skip long introductions and analysis paragraphs. Ask only the displayed question in that turn.
- Keep the emoji fixed: **🍢** for the question and **🔥** for the recommendation reason. Show only the current round's question number: **Question 3** / **第3问**, never a denominator or a forecast such as `3/5`, `Q3 OF 5`, or "two questions left." Do not rotate symbols or add decorative emoji.
- Show the short free-text invitation on every question: **回复字母，或直接说你的想法。** in Chinese, **Reply with a letter, or share your own idea.** in English. It is an answer instruction, not an additional question. Options are suggestions, not an exhaustive list; the recommendation is advice, not a constraint on the user's choice.
- Use the user's language throughout, including the recommendation marker: **（推荐）** in Chinese, **(Recommended)** in English.

## Close a round

Give a short synthesis in the user's language:

- **Recommendation and reason.** State the direction and the most important tradeoff.
- **Decisions and assumptions.** Distinguish what the user chose from your defaults. Include material unresolved risks or blockers; omit empty categories.
- **Next step.** Name one concrete action.

Offer deeper discussion only when a concrete unresolved issue or a high-value improvement could change the plan. Suggest **1–2 specific directions**, each with a brief explanation of what exploring it would resolve or improve. Rank the most useful first. Skip cosmetic details, settled choices, generic "explore more" suggestions, and topics that require unavailable evidence rather than more discussion.

A discussion request alone does not authorize execution. Follow the user's latest direction:

- **Already authorized and ready:** carry out the agreed next action within scope, without asking again or delaying it for optional improvements.
- **Stop or summary requested:** finish with the synthesis. Do not add another choice. Also finish when an explicit all-inclusive cap leaves no room for a closing question.
- **A useful next-step choice remains:** after the synthesis, ask one question using **Next step** / **下一步** instead of a question number. Use the compact format, with 2–3 choices, A recommended, the 🔥 reason, and the free-text invitation. Put execution and deeper discussion in the **same choice**, then wait. Do not ask whether to go deeper and whether to start in separate turns.
  - When execution is concrete, within capabilities, unblocked, and not yet authorized, offer **Start / Go deeper into {specific direction} / Stop** if a worthwhile direction exists; otherwise use **Start / Adjust the plan / Stop**.
  - When a material blocker requires discussion, recommend the relevant deeper direction and omit starting the blocked action. For advice-only requests or an action outside the agent's capabilities, omit Start; offer deeper discussion and Stop only if further discussion has value, otherwise finish with the synthesis.
  - Name the primary direction directly in its choice. If there is a second direction, describe it briefly before the menu and let the user name it in free text; a bare choice letter selects the direction named in that choice. Keep the menu to three choices. Recommend the action best supported by the evidence, rather than always recommending Start.

Interpret the reply against the choices actually displayed:

- **Go deeper:** name the selected focus briefly and begin a new round, again up to five questions unless the user set a different limit. Reset only the round's question number. Carry forward earlier answers, ask only about the selected focus, and close early when possible. Apply this same synthesis-and-choice cycle after every round.
- **Start:** a Start selection or clear affirmative reply to the stated execution choice authorizes only the summarized action and scope. Proceed without another confirmation. Choosing deeper discussion is not execution permission.
- **Adjust:** incorporate the user's corrections without resetting the round's count or inferring execution permission. Ask a further planning question only if it is consequential and fits the remaining budget. If more discussion is needed after the budget is exhausted, offer a concrete deeper direction at the close; do not silently restart. A materially revised proposal may need its own execution choice.
- **Stop:** end without another prompt. Accept custom directions, combined choices, and free-text answers without forcing a letter. Do not create session files unless requested.
