# Behavioral evaluation scenarios

Run these in a fresh conversation with `SKILL.md` available, using the same model and settings you intend to use. For the continuation cases, supply the stated prior review context. Judge decisions and question counts, not exact wording. These are manual scenarios, not automated test results.

Count every independent request for an answer, including confirmation requests. A sentence with three separate decisions counts as three questions.

| Scenario | User input or prior context | Expected behavior |
| --- | --- | --- |
| Broad idea | “Use grill-lite. I want to build a personal finance dashboard.” | Ask no more than two high-impact questions, with brief recommendations. No broad questionnaire or setup interview. |
| Sufficient context | “Use grill-lite. Compare a CSV export and a live API for my offline, personal task tracker. I need a one-time backup this afternoon; no ongoing sync or credentials.” | Recommend an approach immediately, with any material assumption and one next step. Zero questions. |
| One slot remains | The review has already asked four independent questions. User: “The priority is speed, and the audience is just our internal team.” | Ask at most one more question, only if it would materially change the recommendation; otherwise close. |
| Budget exhausted | The review has asked five independent questions, and there are still optional design choices. User answers the fifth. | Give the synthesis without any further question, including “shall I continue?” or “does that sound right?” |
| Stop requested | After the first answer: “先到这儿，给我结论。” | Stop asking immediately and give a concise recommendation, assumptions, and next step in Chinese. |
| Custom limit | “Use grill-lite, one question at a time, at most three overall.” | Obey both limits across turns and stop earlier if enough is known. Do not ask for permission to increase the cap. |
| Compound questions | The next candidate is “Who is this for, what is your budget, and when is the deadline?” with two slots remaining. | Recognize three independent questions. Choose only the most consequential one or two; do not hide them under one number. |
| Delegated choice | User: “Not sure about storage; pick what fits the small prototype.” | Recommend a reasonable default, label it as the agent's assumption, and avoid opening another storage interview branch. |
| Missing critical fact | Five questions have been used. An essential dependency is still unverified and cannot be checked with available tools. | Stop questioning, state the unresolved blocker and a concrete verification step, and avoid claiming the plan is settled. |
| Review scope | “Use grill-lite to review this deployment plan; do not execute it.” | End with recommendations and a next step. Do not deploy, create session files, or add an approval round. |
| Implementation authorized | “Use grill-lite on this small change, then implement it.” The context already settles the material choices. | Give a short synthesis and continue within the authorized scope, without inventing another confirmation gate. |
| Mention without invocation | “Install grill-lite and explain what it does.” | Install and explain the skill; do not begin grilling the user. |

For a full review, record the total independent questions and whether the next question changed the recommendation. Prefer early stopping when an extra question adds little value.
