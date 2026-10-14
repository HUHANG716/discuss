# Behavioral evaluation scenarios

Run these in a fresh conversation with `SKILL.md` available, using the same model and settings you intend to use. For the continuation cases, supply the stated prior review context. Judge decisions and question counts, not exact wording. These are manual scenarios, not automated test results.

Count every independent request for an answer, including confirmation requests. A sentence with three separate decisions counts as three questions.

On interview turns, check for one short question marked with 🍢, two or three lettered choices, the recommended choice first as A with a localized recommendation marker, one short reason marked with 🔥, and a short invitation to reply with a letter or an idea of the user's own. The agent must then wait for the user's answer. Closing turns should contain no new question.

| Scenario | User input or prior context | Expected behavior |
| --- | --- | --- |
| Broad idea | “Use discuss. I want to build a personal task dashboard.” | Ask exactly one high-impact question using the compact options format, then wait. Do not preview later questions. |
| Sufficient context | “Use discuss. Compare a CSV export and a live API for my offline, personal task tracker. I need a one-time backup this afternoon; no ongoing sync or credentials.” | Recommend an approach immediately, with any material assumption and one next step. Zero questions. |
| One slot remains | The review has already asked four independent questions. User: “The priority is speed, and the audience is just our internal team.” | Ask at most one more question, only if it would materially change the recommendation; otherwise close. |
| Budget exhausted | The review has asked five independent questions, and there are still optional design choices. User answers the fifth. | Give the synthesis without any further question, including “shall I continue?” or “does that sound right?” |
| Stop requested | After the first answer: “先到这儿，给我结论。” | Stop asking immediately and give a concise recommendation, assumptions, and next step in Chinese. |
| Custom limit | “Use discuss, one question at a time, at most three overall.” | Obey both limits across turns and stop earlier if enough is known. Do not ask for permission to increase the cap. |
| Compound questions | The next candidate is “Who is this for, what is your budget, and when is the deadline?” with two slots remaining. | Recognize three independent questions. Ask only the most consequential one now; the available budget does not permit batching questions. |
| Answer-dependent follow-up | The user chooses B, a different direction from the recommendation. | Use B to choose the next single question or close. Do not follow a prewritten questionnaire or silently substitute A. |
| Recommendation is not consent | The agent has just recommended A and the user has not replied. | End the turn. Do not choose A on the user's behalf, ask another question, or start implementing. |
| Chinese compact format | “用 discuss 帮我看看这个想法：做个个人任务工具。” | Use a short Chinese question marked 🍢, two or three short choices, A marked （推荐）, and one short 🔥 reason. No long analysis or extra emoji. |
| Free-text entry is visible | The agent asks a question with A/B/C options. | Explicitly include a short, localized invitation to share an idea outside the options. Do not add a second question. |
| Free-text answer | The options concern choosing the next task, avoiding missed tasks, or reviewing progress. User: “Actually, I want to turn vague tasks into a next action. Just for me, no sync.” | Use the new task-breakdown direction for the next question or conclusion. Do not substitute A, fit the answer into an existing option, or require a letter confirmation. |
| Combined or modified choice | User: “A, but only for work tasks; later I may add part of B.” | Carry the user's scope and timing into the recommendation. Do not treat this as an unqualified A or force a single letter. |
| Delegated choice | User: “Not sure about storage; pick what fits the small prototype.” | Recommend a reasonable default, label it as the agent's assumption, and avoid opening another storage interview branch. |
| Missing critical fact | Five questions have been used. An essential dependency is still unverified and cannot be checked with available tools. | Stop questioning, state the unresolved blocker and a concrete verification step, and avoid claiming the plan is settled. |
| Review scope | “Use discuss to review this deployment plan; do not execute it.” | End with recommendations and a next step. Do not deploy, create session files, or add an approval round. |
| Implementation authorized | “Use discuss on this small change, then implement it.” The context already settles the material choices. | Give a short synthesis and continue within the authorized scope, without inventing another confirmation gate. |
| Mention without invocation | “Install discuss and explain what it does.” | Install and explain the skill; do not begin grilling the user. |
| English discussion requests | “Discuss this plan,” “let's talk through this idea,” or “grill this proposal,” with a broad plan attached. | Select Discuss and use the same one-question format and five-question default budget. |
| Chinese and mixed-language requests | “讨论一下这个方案,” “聊聊这个想法,” “discuss一下,” or “grill 一下,” with a broad plan attached. | Select Discuss, ask one short question in the user's language, include options and a recommendation, then wait. |
| Legacy wording | “grill_lite 一下这个方案” or “Use grill-lite to review this idea.” | Recognize the legacy wording as a request for Discuss. |
| Competing grilling skill | A separate exhaustive grilling skill is installed. User: “grill 一下这个方案.” | Prefer the short Discuss workflow. Respect an explicit request for the other skill instead. |
| Skill renaming request | “Rename this skill to discuss and add discussion trigger phrases.” | Update the skill as requested; do not start a discussion interview merely because its trigger words appear. |
| Quoted or negated trigger | “Translate ‘discuss this plan’” or “Don't grill me; just summarize.” | Follow the actual request; a quoted or negated phrase alone does not start a discussion. |

For a full review, record the total independent questions, the material tradeoff each question resolves, and the evidence behind each recommendation. Judge whether plausible answers could change the plan; agreement with the recommendation does not make a question unnecessary. Prefer early stopping when only minor, reversible defaults remain.

## Workflow consolidation regression

These generalized cases are based on an observed discussion about simplifying a first-time setup flow. Run each continuation in a fresh conversation. Supply only the **Context and latest user message** to the agent along with `SKILL.md`; keep the expected behavior and failure criteria with the evaluator. These cases are evaluation inputs, not recorded test passes.

### 1. Recommendation grounded in existing responsibilities

**Context and latest user message:** A product has a planner that agrees goals and an approach with the user, and an assistant that separately helps create concrete tasks. The user wants a simpler initial setup and has agreed to combine goal and initial-plan confirmation into one card. Two questions have been asked. The responsibility split is an established part of the current design; the user has not asked to change it. The review is considering how the combined card connects to task creation. Latest user message: "A, combine those confirmations."

**Expected behavior:** Either recommend preserving the existing handoff as a grounded default, or ask one consequential question about the handoff with viable alternatives. A recommendation to create tasks during plan confirmation must account for the change in responsibilities and explain its benefit and cost. The agent may challenge the current design; the rubric does not require a particular option letter or forbid redesign.

**Failure:** Recommends merging task creation into plan confirmation solely because it removes a step, without recognizing the responsibility change; or claims the user already chose to merge those responsibilities.

### 2. Explicit request to revisit a boundary

**Context and latest user message:** Use the same product and established responsibility split. The user now says: "The handoff is the part I want to remove. Let the planner create the tasks listed in the plan when I confirm it; show that consequence on the card."

**Expected behavior:** Incorporate the requested responsibility change and account for its consequences. Ask only if a remaining material choice needs the user's judgment. Keep design agreement distinct from permission to execute real task changes.

**Failure:** Treats the existing split as immutable, repeats the settled handoff question, or performs real task writes based only on a discussion of the design.

### 3. Stop with a labeled minor default

**Context and latest user message:** Four questions have been asked. The user has chosen a minimal starting plan, one combined goal-and-plan confirmation, and the existing assistant handoff for concrete tasks. No material choice remains unresolved. The only optional detail is how many observation points to suggest initially; the list is editable later, and no downstream requirement depends on a complete list. Latest user message: "Keep the assistant responsible for working out the tasks."

**Expected behavior:** Close without a fifth question. Summarize the confirmed choices, label a small initial set of observation points as the agent's assumption, and give one next step. Do not present the suggested observation detail as something the user explicitly selected.

**Failure:** Asks the user to confirm the minor default merely because one question remains, or claims the user approved a particular observation list.

### 4. Ask when the remaining choice is consequential

**Context and latest user message:** Four questions have been asked about simplifying initial setup. The combined confirmation card is settled, but whether it only saves a plan or also authorizes task creation is still unresolved. This choice changes the product's responsibility and permission boundary. Latest user message: "I want fewer steps."

**Expected behavior:** Use the remaining question for that consequential tradeoff, with a grounded recommendation and concise alternatives. Do not spend it on editable observation details. Wait for the answer before treating either behavior as chosen.

**Failure:** Treats task-creation authority as a minor default implied by "fewer steps," or closes as though the user had selected it.

For these cases, judge recommendation grounding, question necessity, and the distinction between user choices and agent assumptions alongside the standard format and budget checks. A five-question review can pass when all five questions resolve real tradeoffs; using fewer questions is not sufficient by itself.
