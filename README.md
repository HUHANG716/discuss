<p align="center">
  <img src="assets/readme-hero.svg" alt="Grill Lite — Ask what matters. Then move. One short question at a time, with options and a recommendation. Up to five overall, with an early finish when the decision is clear." width="100%">
</p>

<p align="center">
  <strong>A focused second opinion for the plan you already have.</strong><br>
  Bring an idea. Get a few sharp questions, a recommendation, and a concrete next step.
</p>

<p align="center">
  <a href="README.zh-CN.md">简体中文</a> ·
  <a href="SKILL.md">Read the skill</a> ·
  <a href="https://github.com/HUHANG716/grill-lite/releases/latest">Download</a> ·
  <a href="LICENSE">MIT license</a>
</p>

---

## Get started

Install with the [Skills CLI](https://github.com/vercel-labs/skills):

```sh
npx skills add HUHANG716/grill-lite --skill grill-lite
```

Then bring your plan to your agent. In Codex:

```text
Use $grill-lite to review this plan: [your plan here].
```

<details>
<summary><strong>Codex: install globally</strong></summary>

```sh
npx skills add HUHANG716/grill-lite --skill grill-lite --agent codex --global
```

</details>

## See a review from start to finish

*An illustrative conversation. One useful answer can be enough.*

**You**

> I want to rebuild my personal task tracker as a web app. Use grill-lite.

**Grill Lite**

> ❓ **1/5: What should the first version solve?**
>
> - **A. Choosing the next task (Recommended)**
> - B. Missing tasks
> - C. Reviewing progress
>
> 💡 A gives the first version one clear job.

**You**

> Choosing what to do next. Just for me, no sync. It could be much smaller.

**Grill Lite · Done**

> **Recommendation:** prototype a local daily-priority view before a full rebuild.
>
> **Your decisions:** personal use, no sync, focus on the next task.
>
> **My assumption:** manual task entry is enough for the first version.
>
> **Next step:** sketch an inbox and today's top three tasks on one screen.

The review ends after one question because there is enough to recommend a direction.

## Small budget. Useful pressure.

| Rule | What it means for you |
| --- | --- |
| **One question at a time** | Answer one decision, then get the next question if needed. |
| **2–3 options, one recommended** | Short choices, with the recommended option clearly marked first. |
| **Up to 5 per review** | One budget across the whole conversation, including follow-ups. |
| **Fixed ❓ / 💡 format** | A short question and a brief reason you can scan immediately. |
| **Defaults for minor choices** | The agent handles reversible details and labels its assumptions. |
| **An early finish** | Enough context means a conclusion, even with questions left in the budget. |

Grill Lite focuses on choices that change direction, scope, or viability. It still challenges weak assumptions and calls out consequential contradictions. Each turn asks about one decision, offers options, and waits for your answer. Reply with a letter or describe your own choice.

## Set your own pace

| Say this | Get this |
| --- | --- |
| `Three questions overall.` | A smaller question budget, still asked one by one. |
| `Focus on what could make the plan fail.` | Questions aimed at the most consequential risks. |
| `Give me your conclusion.` | An immediate synthesis and next step. |
| `Review this, then implement it.` | A review followed by work within the scope you authorized. |

The default limit is a ceiling, not a quota. A sufficiently clear plan can need **zero questions**. Ask explicitly when you want to go deeper.

## Fits your existing agent

The core is one [SKILL.md](SKILL.md): plain Markdown, with no runtime scripts, API key, or required external service. Use it with agents that support the Agent Skills format. The Skills CLI supports Codex, Claude Code, Cursor, and other agents; select yours during installation.

The conversation follows your language. You can use the English instructions and ask in Chinese:

```text
用 $grill-lite 帮我过一下这个方案，总共最多三个问题。
```

<details>
<summary><strong>Manual installation</strong></summary>

Copy `SKILL.md` and the optional `agents/` folder into a `grill-lite` directory under your agent's skills directory. Keep `LICENSE` with redistributed copies.

For Codex, `~/.agents/skills/grill-lite/` is a user-level location. See the [official skill documentation](https://learn.chatgpt.com/docs/build-skills).

</details>

<details>
<summary><strong>How the question limit works</strong></summary>

The budget covers the entire review. Each question addresses one decision, with two or three choices and a recommendation, and the agent waits for your answer before continuing. Independent requests for an answer count individually, including setup and confirmation questions. At the limit, material unresolved blockers belong in the conclusion.

This is a model instruction, not a programmatic counter. The [manual evaluation scenarios](EVALS.md) help check counting, early stopping, custom limits, and execution scope. They are an evaluation rubric, not a claim of automated behavioral test coverage.

</details>

## Make it sharper

Share a small example where a question changed your decision, or where the agent kept asking after the answer was already clear. [Open an issue](https://github.com/HUHANG716/grill-lite/issues) or propose a focused improvement.

Good contributions help the next user reach a sound decision with less unnecessary back-and-forth.

---

Inspired by [Matt Pocock's grilling skill](https://github.com/mattpocock/skills/blob/main/skills/productivity/grilling/SKILL.md). Independently written, with a bounded question budget and an explicit early stopping rule.

[MIT licensed](LICENSE). Use it, adapt it, and share it.
