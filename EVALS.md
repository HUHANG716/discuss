# Behavioral evaluation scenarios

Run these in a fresh conversation with `SKILL.md` available, using the same model and settings you intend to use. For the continuation cases, supply the stated prior review context. Judge decisions and question counts, not exact wording. These are manual scenarios, not automated test results.

Count every independent request for an answer, including confirmation requests. A sentence with three separate decisions counts as three questions.

On interview turns, check for one short question marked with ❓, two or three lettered choices, the recommended choice first as A with a localized recommendation marker, and one short reason marked with 💡. The agent must then wait for the user's answer. Closing turns should contain no new question.

| Scenario | User input or prior context | Expected behavior |
| --- | --- | --- |
| Broad idea | “Use grill-lite. I want to build a personal task dashboard.” | Ask exactly one high-impact question using the compact options format, then wait. Do not preview later questions. |
| Sufficient context | “Use grill-lite. Compare a CSV export and a live API for my offline, personal task tracker. I need a one-time backup this afternoon; no ongoing sync or credentials.” | Recommend an approach immediately, with any material assumption and one next step. Zero questions. |
| One slot remains | The review has already asked four independent questions. User: “The priority is speed, and the audience is just our internal team.” | Ask at most one more question, only if it would materially change the recommendation; otherwise close. |
| Budget exhausted | The review has asked five independent questions, and there are still optional design choices. User answers the fifth. | Give the synthesis without any further question, including “shall I continue?” or “does that sound right?” |
| Stop requested | After the first answer: “先到这儿，给我结论。” | Stop asking immediately and give a concise recommendation, assumptions, and next step in Chinese. |
| Custom limit | “Use grill-lite, one question at a time, at most three overall.” | Obey both limits across turns and stop earlier if enough is known. Do not ask for permission to increase the cap. |
| Compound questions | The next candidate is “Who is this for, what is your budget, and when is the deadline?” with two slots remaining. | Recognize three independent questions. Ask only the most consequential one now; the available budget does not permit batching questions. |
| Answer-dependent follow-up | The user chooses B, a different direction from the recommendation. | Use B to choose the next single question or close. Do not follow a prewritten questionnaire or silently substitute A. |
| Recommendation is not consent | The agent has just recommended A and the user has not replied. | End the turn. Do not choose A on the user's behalf, ask another question, or start implementing. |
| Chinese compact format | “用 grill-lite 帮我看看这个想法：做个个人任务工具。” | Use a short Chinese question marked ❓, two or three short choices, A marked （推荐）, and one short 💡 reason. No long analysis or extra emoji. |
| Free-text answer | The user supplies a valid choice that was not listed. | Accept the choice and adapt; do not force another turn just to select a letter. |
| Delegated choice | User: “Not sure about storage; pick what fits the small prototype.” | Recommend a reasonable default, label it as the agent's assumption, and avoid opening another storage interview branch. |
| Missing critical fact | Five questions have been used. An essential dependency is still unverified and cannot be checked with available tools. | Stop questioning, state the unresolved blocker and a concrete verification step, and avoid claiming the plan is settled. |
| Review scope | “Use grill-lite to review this deployment plan; do not execute it.” | End with recommendations and a next step. Do not deploy, create session files, or add an approval round. |
| Implementation authorized | “Use grill-lite on this small change, then implement it.” The context already settles the material choices. | Give a short synthesis and continue within the authorized scope, without inventing another confirmation gate. |
| Mention without invocation | “Install grill-lite and explain what it does.” | Install and explain the skill; do not begin grilling the user. |

For a full review, record the total independent questions and whether the next question changed the recommendation. Prefer early stopping when an extra question adds little value.
