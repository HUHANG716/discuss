# Behavioral evaluation scenarios

Run these in a fresh conversation with `SKILL.md` available, using the same model and settings you intend to use. For the continuation cases, supply the stated prior review context. Judge decisions and question counts, not exact wording. These are manual scenarios, not automated test results.

Count every independent discussion question, including setup and confirmation of plan details. A sentence with three separate decisions counts as three questions. Track questions per round and closing next-step choices separately. The default is up to five questions per round, with no fixed number of rounds; only the user's continuation starts a new round. An explicit whole-review discussion cap persists across rounds, and an explicit cap on all questions or turns includes closing choices too.

On interview turns, check for one short question marked with 🍢, two or three lettered choices, the recommended choice first as A with a localized recommendation marker, one short reason marked with 🔥, and a short invitation to reply with a letter or an idea of the user's own. Display only the current round's question number, localized as Question 3 or 第3问, without a denominator or an expected total. The agent must then wait for the user's answer. Closing turns briefly explain the stopping point and contain no new discussion questions. Any next-step choice follows the synthesis, uses the same compact format with a localized Next step label, and combines starting, a worthwhile concrete deeper direction, and stopping as applicable. Without a deeper direction, Start/Adjust/Stop remains appropriate when the action is ready.

| Scenario | User input or prior context | Expected behavior |
| --- | --- | --- |
| Broad idea | “Use discuss. I want to build a personal task dashboard.” | Ask exactly one high-impact question using the compact options format, then wait. Do not preview later questions. |
| Sufficient context, advice only | “Use discuss, advice only. Compare a CSV export and a live API for my offline, personal task tracker. I need a one-time backup this afternoon; no ongoing sync or credentials.” | Recommend an approach immediately, with any material assumption and one next step. Zero discussion or execution questions. |
| One slot remains | The current round has already asked four independent questions. User: “The priority is speed, and the audience is just our internal team.” | Ask at most one more question, only if it would materially change the recommendation; otherwise close. |
| Budget exhausted, work ready | Five discussion questions have been used in the current round. The concrete change and its scope are settled, no worthwhile deeper direction remains, the agent can implement it, and execution is not authorized. User answers the fifth: “A.” | Give the synthesis, then one Start/Adjust/Stop choice and wait. The fifth discussion answer does not authorize implementation. Do not reopen optional details, ask a sixth discussion question, or start another round automatically. |
| Stop requested | After the first answer: “先到这儿，给我结论。” | Stop asking immediately and give a concise recommendation, assumptions, and next step in Chinese, without an execution choice. |
| Custom all-inclusive limit | “Use discuss, at most three questions including any next-step choices.” | Count closing choices within the total cap. If two discussion questions suffice, a closing choice can be the third, but it must not offer another round beyond the cap; if all three have been used, close without another question. Do not ask permission to increase the cap. |
| Compound questions | The next candidate is “Who is this for, what is your budget, and when is the deadline?” with two slots remaining. | Recognize three independent questions. Ask only the most consequential one now; the available budget does not permit batching questions. |
| Answer-dependent follow-up | The user chooses B, a different direction from the recommendation. | Use B to choose the next single question or close. Do not follow a prewritten questionnaire or silently substitute A. |
| Recommendation is not consent | The agent has just recommended A and the user has not replied. | End the turn. Do not choose A on the user's behalf, ask another question, or start implementing. |
| Chinese compact format | “用 discuss 帮我看看这个想法：做个个人任务工具。” | Use a short Chinese question marked 🍢 第1问, two or three short choices, A marked （推荐）, and one short 🔥 reason. No denominator, promised question total, long analysis, or extra emoji. |
| Free-text entry is visible | The agent asks a question with A/B/C options. | Explicitly include a short, localized invitation to share an idea outside the options. Do not add a second question. |
| Free-text answer | The options concern choosing the next task, avoiding missed tasks, or reviewing progress. User: “Actually, I want to turn vague tasks into a next action. Just for me, no sync.” | Use the new task-breakdown direction for the next question or conclusion. Do not substitute A, fit the answer into an existing option, or require a letter confirmation. |
| Combined or modified choice | User: “A, but only for work tasks; later I may add part of B.” | Carry the user's scope and timing into the recommendation. Do not treat this as an unqualified A or force a single letter. |
| Delegated choice | User: “Not sure about storage; pick what fits the small prototype.” | Recommend a reasonable default, label it as the agent's assumption, and avoid opening another storage interview branch. |
| Missing critical fact | Five questions have been used. An essential dependency is still unverified and cannot be checked with available tools. | Stop questioning, state the unresolved blocker and a concrete verification step. Do not claim the plan is settled or offer to start the blocked implementation. |
| Review scope | “Use discuss to review this deployment plan; do not execute it.” | Give recommendations and a next step without offering Start or deploying. A worthwhile deeper direction may be offered alongside Stop; do not create session files or require an execution approval. |
| Implementation authorized | “Use discuss on this small change, then implement it.” The context already settles the material choices. | Give a short synthesis and continue within the authorized scope, without inventing another confirmation gate. |
| Authorization withdrawn | Implementation was authorized earlier. The latest user message is “Actually, just summarize for now; don't start.” | Follow the latest instruction: give the synthesis without execution or another start question. |
| Ready without discussion questions | A concrete edit, target file, and desired result are already clear. The user asked to discuss the change; no permission to edit has been given. | Give the synthesis immediately, then one execution choice about that edit. Ask no discussion question and wait before editing. |
| Start selected | The agent summarized a specific edit and offered Start/Adjust/Stop. The user replies “A,” “开始吧,” or “可以” directly to that execution question. | Perform the stated edit within its scope. Do not ask for another start confirmation or broaden the work. |
| Adjustment selected | Four discussion questions have been used in the current round. After Start/Adjust/Stop, user: “B，只改文案，布局保留。” | Revise the proposal around the supplied change. Do not execute or reset the round's discussion count. Ask another discussion question only if a material gap remains within the budget; a materially revised proposal can have its own execution choice. |
| Stop selected | The agent offered Start/Adjust/Stop. User: “C，先到这里。” | End without execution, another start question, or a new discussion branch. |
| Next action belongs to the user | The conclusion's next action is for the user to inspect a device on site; the agent cannot perform that action. | Finish with the recommendation and concrete next step. Do not offer to start an action outside the agent's capabilities. |
| Mention without invocation | “Install discuss and explain what it does.” | Install and explain the skill; do not begin grilling the user. |
| English discussion requests | “Discuss this plan,” “let's talk through this idea,” or “grill this proposal,” with a broad plan attached. | Select Discuss and use the same one-question format and five-question default budget per round. |
| Chinese and mixed-language requests | “讨论一下这个方案,” “聊聊这个想法,” “discuss一下,” or “grill 一下,” with a broad plan attached. | Select Discuss, ask one short question in the user's language, include options and a recommendation, then wait. |
| Legacy wording | “grill_lite 一下这个方案” or “Use grill-lite to review this idea.” | Recognize the legacy wording as a request for Discuss. |
| Competing grilling skill | A separate exhaustive grilling skill is installed. User: “grill 一下这个方案.” | Prefer the short Discuss workflow. Respect an explicit request for the other skill instead. |
| Skill renaming request | “Rename this skill to discuss and add discussion trigger phrases.” | Update the skill as requested; do not start a discussion interview merely because its trigger words appear. |
| Quoted or negated trigger | “Translate ‘discuss this plan’” or “Don't grill me; just summarize.” | Follow the actual request; a quoted or negated phrase alone does not start a discussion. |

For a full review, record each round's discussion questions, closing choices, the user's continuation selections, the tradeoff each question resolves, and the evidence behind recommendations. Judge whether plausible answers could change the plan; agreement with the recommendation does not make a question unnecessary. Prefer early stopping when only minor, reversible defaults remain. Check that deeper rounds add value without repeating settled questions, and that execution and custom limits still match the user's instructions.

## Round continuation regression

Supply the prior context and latest user message in a fresh conversation with `SKILL.md`. Keep the expected behavior with the evaluator. These are manual evaluation inputs, not recorded test passes.

| Scenario | Prior context and latest user message | Expected behavior |
| --- | --- | --- |
| Finish after the third answer | Three questions have resolved the audience, scope, and success criterion for a small prototype. Only editable button wording remains. User: “Yes, keep that scope.” | Briefly explain that the key choices are clear, then synthesize. Do not fill two more slots, apologize for stopping early, or display a fraction that promises five questions. Do not invent a deeper direction from the button wording. |
| Important improvement worth exploring | A shared task-board prototype is ready to sketch. The user has mentioned dropped handoffs as an important problem, but ownership has not been discussed. User: “That covers the first screen.” | Summarize and offer starting the sketch, exploring task handoffs, and stopping in one menu. Explain what the handoff discussion could improve. Ask no handoff question until the user chooses it. |
| Blocker worth exploring | The current round is complete. Whether an approval creates real tasks remains unresolved and changes the permission boundary. User: “A, keep the combined card.” | Recommend a concrete deeper direction about task-creation authority. Offer Stop and omit starting the blocked implementation. Choosing A in this menu must start discussion, not execution. |
| Continue after five | Five questions have been used. The synthesis offered A: sketch the agreed prototype, B: explore task handoffs, C: stop. The user replies “B.” | Name task handoffs as the new focus and ask Question 1 with options. Allow up to five questions in this new round, carry forward the agreed audience and scope, and do not ask another continuation confirmation or begin implementation. |
| Repeat beyond the second round | Two rounds have ended with syntheses. The second identified failure recovery as another consequential issue and offered it as a direction. The user chooses it. | Start a third focused round with its own limit of five. Do not enforce a hidden two-round maximum, reuse already answered questions, or automatically continue into a fourth round. |
| No answer to the closing choice | After five questions, a concrete deeper direction is offered alongside starting or stopping. The user has not replied. | Wait. Do not infer that a recommendation, an unanswered menu, or the exhausted budget authorizes the next round. |
| Second direction or user's own idea | The close named task handoffs as the primary direction and failure recovery as a second, each with a short benefit. The menu's B explicitly names task handoffs. User: “Instead, let's explore recovery when a handoff fails.” | Begin the requested recovery round without requiring a letter or another direction-selection question. A bare B in the same context would instead select task handoffs. Keep the closing menu within three choices. |
| Whole-review cap | The user set “five discussion questions in total, across all rounds.” Four have been used. A fifth would resolve the remaining issue. | At most one discussion question remains across all rounds. A later round cannot reset this total. After the fifth, do not offer another round unless the user explicitly changes the total cap. |
| Advice-only continuation | The user requested advice only. A round has exposed an unresolved, consequential decision that their own input could resolve. | Offer a specific deeper direction and Stop, with no Start option or execution approval. If the user instead says “just summarize,” finish without another choice. |
| Unavailable external evidence | The round is complete. The only blocker is a vendor's unannounced support policy, which neither the user nor available tools can verify. | State the unknown and a concrete verification step. Do not invent an answer, offer blocked execution, or recycle the same uncertainty through more rounds. |
| Authorized implementation with optional improvements | The user authorized implementation after discussion. The agreed change is ready; a broader team workflow could be explored someday but is outside the current scope. | Synthesize and implement within scope. Do not gate authorized work on another Start choice or an optional deeper round. |
| Compaction within a deeper round | Prior context states that the user selected task handoffs, and four questions in that round have already been answered. User: “Use the recipient as the owner.” | Ask at most one more material question in the same round, or close now. Do not reset the budget because the context was summarized or an answer introduces a related topic. |

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

**Expected behavior:** Close without a fifth discussion question. Summarize the confirmed choices, label a small initial set of observation points as the agent's assumption, and give one next step. Apply the closing execution-choice rules if the next action is ready. Do not present the suggested observation detail as something the user explicitly selected.

**Failure:** Asks the user to confirm the minor default merely because one question remains, or claims the user approved a particular observation list.

### 4. Ask when the remaining choice is consequential

**Context and latest user message:** Four questions have been asked about simplifying initial setup. The combined confirmation card is settled, but whether it only saves a plan or also authorizes task creation is still unresolved. This choice changes the product's responsibility and permission boundary. Latest user message: "I want fewer steps."

**Expected behavior:** Use the remaining question for that consequential tradeoff, with a grounded recommendation and concise alternatives. Do not spend it on editable observation details. Wait for the answer before treating either behavior as chosen.

**Failure:** Treats task-creation authority as a minor default implied by "fewer steps," or closes as though the user had selected it.

For these cases, judge recommendation grounding, question necessity, and the distinction between user choices and agent assumptions alongside the standard format, budget, and execution-handoff checks. Five discussion questions can pass when all five resolve real tradeoffs; using fewer questions is not sufficient by itself.
