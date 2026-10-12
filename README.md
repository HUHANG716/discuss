# Grill Lite

[中文说明](README.zh-CN.md) · [Skill instructions](SKILL.md) · [MIT license](LICENSE)

A lightweight agent skill for pressure-testing a plan, idea, or decision. Ask a few consequential questions, then give a recommendation and a concrete next step.

## The rules

- **1–2 questions per turn; at most 5 per review** by default.
- Stop earlier when the context is sufficient. A clear request can need zero questions.
- Ask about choices that change direction, scope, or viability.
- Give a recommendation with each question. Set sensible defaults for minor choices and label assumptions.
- Count separate decisions, including questions hidden inside a sentence.
- Stop immediately when the user asks for a conclusion or says to proceed.
- Finish with a recommendation, the important decisions and assumptions, and one next step.

The limit covers the whole review, not each message. Users can set a different limit or explicitly ask to go deeper. The skill does not automatically create session files or require extra approval rounds.

## Install

With the [Skills CLI](https://github.com/vercel-labs/skills):

```sh
npx skills add HUHANG716/grill-lite --skill grill-lite
```

Install globally for Codex:

```sh
npx skills add HUHANG716/grill-lite --skill grill-lite --agent codex --global
```

For other supported agents, select your agent in the installer. The runtime instructions are plain Markdown and do not require scripts, an API key, or a particular tool.

To install manually, copy `SKILL.md` and the optional `agents/` folder into a `grill-lite` directory under your agent's skills directory. Keep `LICENSE` with redistributed copies. For Codex, `~/.agents/skills/grill-lite/` is a user-level location. See the [official skill documentation](https://learn.chatgpt.com/docs/build-skills).

## Use

In Codex:

```text
Use $grill-lite to pressure-test my plan to migrate a small app to Kotlin Multiplatform.
```

Or ask naturally:

```text
Give this idea a light grilling. Ask only what could change the direction.
```

```text
用 grill-lite 帮我过一下这个方案，每轮一个问题，总共最多三个。
```

You can stop at any point: “Give me your conclusion,” “That's enough,” or “先给结论”. If you also request implementation, the agent continues within that authorization after the review; asking for a review alone does not start implementation.

## Example

**User:** I'm thinking of building a personal task manager. Use grill-lite.

**Agent:** Which recurring problem should the first version solve: forgetting tasks, choosing what to do next, or tracking progress? I recommend choosing what to do next, because that gives the first version a specific job.

**User:** Choosing what to do next. It's just for me, and I don't need sync.

**Agent:** Recommendation: start with a local daily-priority view. You chose a personal tool focused on choosing the next task, with no sync. My assumption is that manual task entry is enough for the first version. Next step: sketch one screen with a task inbox and today's top three tasks.

One useful answer can be enough. There is no requirement to use all five questions.

## Check or improve it

Use the [behavioral scenarios](EVALS.md) to check question counting, early stopping, user overrides, and scope. These are a manual evaluation rubric, not a claim of automated behavioral test coverage. The question budget is an instruction to the model, not a programmatic enforcement mechanism.

Contributions should make decisions easier with fewer unnecessary questions. Explain the observed failure and include a small example before adding a rule.

## Credits and license

Inspired by [Matt Pocock's grilling skill](https://github.com/mattpocock/skills/blob/main/skills/productivity/grilling/SKILL.md). Grill Lite uses independently written instructions with a bounded question budget and an explicit early stopping rule.

Released under the [MIT license](LICENSE).
