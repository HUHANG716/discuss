<p align="center">
  <img src="assets/readme-hero.svg" alt="Discuss — Ask what matters. Then move. One short question at a time, with options and a recommendation. Up to five questions per round; summarize early, then choose to act, explore a useful direction, or stop." width="100%">
</p>

<p align="center">
  <strong>A focused second opinion for the plan you already have.</strong><br>
  Bring an idea. Get a few sharp questions, a recommendation, and a concrete next step.
</p>

<p align="center">
  <a href="README.zh-CN.md">简体中文</a> ·
  <a href="SKILL.md">Read the skill</a> ·
  <a href="https://github.com/HUHANG716/discuss/releases/latest">Download</a> ·
  <a href="LICENSE">MIT license</a>
</p>

---

## Get started

Install with the [Skills CLI](https://github.com/vercel-labs/skills):

```sh
npx skills add HUHANG716/discuss --skill discuss
```

Then bring your plan to your agent. In Codex:

```text
Use $discuss to review this plan: [your plan here].
```

You can also say `discuss this plan`, `let's talk through this idea`, or `grill this proposal`. The same short discussion applies.

Previously published as `grill-lite`. The skill name and installation folder are now `discuss`.

<details>
<summary><strong>Codex: install globally</strong></summary>

```sh
npx skills add HUHANG716/discuss --skill discuss --agent codex --global
```

</details>

## See a review from start to finish

*An illustrative conversation. One useful answer can be enough.*

**You**

> I want to rebuild my personal task tracker as a web app. Use discuss.

**Discuss**

> 🍢 **Question 1: What should the first version solve?**
>
> - **A. Choosing the next task (Recommended)**
> - B. Missing tasks
> - C. Reviewing progress
>
> 🔥 A gives the first version one clear job.
>
> Reply with a letter, or share your own idea.

**You**

> Actually, I want to turn vague tasks into a clear next action. Just for me, no sync.

**Discuss · Conclusion**

> That's enough to sketch the first version.
>
> **Recommendation:** prototype a local task-breakdown view that turns a vague task into a concrete next action.
>
> **Your decisions:** just for you, no sync, focus on breaking tasks down.
>
> **My assumption:** you can write the next action yourself in the first version.
>
> **Next step:** sketch a task title, its next action, and a start button on one screen.
>
> 🍢 **Next step: Shall I draft that one-screen wireframe?**
>
> - **A. Draft the wireframe (Recommended)**
> - B. Adjust the plan (describe the changes)
> - C. Stop here
>
> 🔥 A wireframe makes the agreed flow concrete with little effort.
>
> Reply with a letter, or share your own idea.

Your answer introduces a direction outside the listed options. The agent follows it and concludes after one discussion question. It then waits for your execution choice before drafting the wireframe.

## Go deeper where it helps

Each round ends with a synthesis. If an unresolved issue or a valuable improvement deserves attention, Discuss names a concrete direction and explains what exploring it would achieve. You choose it alongside starting or stopping.

For example, an agreed team-board prototype can be sketched now, while task handoffs could be explored before expanding it:

> **Worth exploring:** task handoffs — clarify who takes responsibility when work changes hands.
>
> 🍢 **Next step: What should we do next?**
>
> - **A. Sketch the agreed prototype (Recommended)**
> - B. Explore task handoffs
> - C. Stop here
>
> 🔥 A sketch lets you test the agreed flow before adding team rules.
>
> Reply with a letter, or share your own idea.

Choose B to begin a focused round of **up to five questions**, carrying forward earlier decisions. The round starts at **Question 1** and can finish as soon as enough is clear. It ends with the same synthesis and next-step choice whenever useful. There is no fixed number of rounds; each continuation is your choice.

If a blocker must be resolved first, Discuss recommends exploring that issue and leaves out starting the blocked action. If no worthwhile direction remains, it offers the usual Start/Adjust/Stop choice when work is ready, or simply concludes when no choice is needed.

## Small budget. Useful pressure.

| Rule | What it means for you |
| --- | --- |
| **One question at a time** | Answer one decision, then get the next question if needed. |
| **2–3 options, one recommended** | Short choices, with the recommended option clearly marked first. |
| **Your own ideas welcome** | Every question invites free text. Combine, change, or go beyond the options. |
| **Up to 5 questions per round** | Often fewer. The agent summarizes before you choose another round. |
| **Fixed 🍢 / 🔥 format** | A short question and reason; only the current question number is shown. |
| **Defaults for minor choices** | The agent handles reversible details and labels its assumptions. |
| **An early finish** | Enough context means a conclusion, even with questions left in the budget. |
| **A useful next-step choice** | Start, explore a specific direction, or stop. Prior execution approval lets the agent continue directly. |

Discuss focuses on choices that change direction, scope, or viability. Recommendations use the known constraints and your confirmed decisions; a recommendation to change existing responsibilities or scope includes its benefit and cost. Minor, reversible details can become labeled assumptions instead of another question. Each question offers options and waits for your answer. The recommendation is advice; your answer guides what comes next.

## Set your own pace

| Say this | Get this |
| --- | --- |
| `Three discussion questions overall.` | A total discussion cap that persists across rounds. |
| `Go deeper into failure recovery.` | A focused new round that builds on earlier decisions. |
| `Focus on what could make the plan fail.` | Questions aimed at the most consequential risks. |
| `Give me your conclusion.` | An immediate synthesis and next step. |
| `Review this, then implement it.` | A review followed by work within the scope you authorized. |

The default limit is a ceiling, not a quota. A sufficiently clear plan can need **zero discussion questions**. You see **Question 3**, not a promised total; finishing there is normal. A deeper round starts only when you choose or request it.

## Fits your existing agent

The core is one [SKILL.md](SKILL.md): plain Markdown, with no runtime scripts, API key, or required external service. Use it with agents that support the Agent Skills format. The Skills CLI supports Codex, Claude Code, Cursor, and other agents; select yours during installation.

Questions and recommendations follow your language. To review a plan with the default limit:

```text
Use $discuss to review this plan. Ask one question at a time, up to five per round, and let me choose whether to go deeper.
```

<details>
<summary><strong>Manual installation</strong></summary>

Copy `SKILL.md` and the optional `agents/` folder into a `discuss` directory under your agent's skills directory. Keep `LICENSE` with redistributed copies.

For Codex, `~/.agents/skills/discuss/` is a user-level location. See the [official skill documentation](https://learn.chatgpt.com/docs/build-skills).

</details>

<details>
<summary><strong>How the question limit works</strong></summary>

The default budget is up to five discussion questions per round. Each addresses one decision, with two or three choices and a recommendation, and the agent waits for your answer. Setup questions and confirmation of plan details count too. The agent tracks the cap internally and shows only the current question number. It explains an early finish briefly and summarizes instead of filling unused slots.

One closing next-step choice is separate from the default discussion budget; it cannot contain extra planning questions. A selected deeper direction opens a new round with a fresh question count and the earlier decisions intact. Explicit limits across the whole review still apply across rounds, and an explicit cap on all questions or turns includes closing choices. Reaching a cap never starts another round automatically.

The agent suggests one or two worthwhile directions with a brief reason for each. The primary direction appears directly in the next-step choice; you can name the second or your own idea in free text. Prior execution authorization lets the agent continue directly when ready. Advice-only requests can still explore useful directions, but do not offer Start. A stop or summary request ends the discussion without another choice. An unavailable fact remains a stated blocker, not a reason to keep asking.

This is a model instruction, not a programmatic counter. The [manual evaluation scenarios](EVALS.md) help check rounds, numbering, early stopping, custom limits, and execution scope. They are an evaluation rubric, not a claim of automated behavioral test coverage.

</details>

## Make it sharper

Share a small example where a question changed your decision, or where the agent kept asking after the answer was already clear. [Open an issue](https://github.com/HUHANG716/discuss/issues) or propose a focused improvement.

Good contributions help the next user reach a sound decision with less unnecessary back-and-forth.

---

Inspired by [Matt Pocock's grilling skill](https://github.com/mattpocock/skills/blob/main/skills/productivity/grilling/SKILL.md). Independently written, with a bounded question budget and an explicit early stopping rule.

[MIT licensed](LICENSE). Use it, adapt it, and share it.
