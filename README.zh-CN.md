<p align="center">
  <img src="assets/readme-hero.svg" alt="Grill Lite：问到关键处，就往前走。每轮一到两题，默认全程最多五题，信息足够就提前收尾。" width="100%">
</p>

<p align="center">
  <strong>问到关键处，就往前走。</strong><br>
  带上你的方案，聊清几个关键问题，得到建议和一个具体的下一步。
</p>

<p align="center">
  <a href="README.md">English</a> ·
  <a href="SKILL.md">技能规则</a> ·
  <a href="https://github.com/HUHANG716/grill-lite/releases/latest">下载安装包</a> ·
  <a href="LICENSE">MIT 许可证</a>
</p>

---

## 先用起来

通过 [Skills CLI](https://github.com/vercel-labs/skills) 安装：

```sh
npx skills add HUHANG716/grill-lite --skill grill-lite
```

然后把方案交给助手。在 Codex 中可以这样说：

```text
用 $grill-lite 帮我过一下这个方案：……
```

<details>
<summary><strong>Codex：全局安装</strong></summary>

```sh
npx skills add HUHANG716/grill-lite --skill grill-lite --agent codex --global
```

</details>

## 一次完整的讨论，可以这么短

*以下为示例对话。一次有效回答就可能足够。*

**你**

> 我想把个人任务管理工具重做成一个 Web 应用，用 grill-lite 帮我看看。

**Grill Lite · 第 1 题 / 最多 5 题**

> 现在最值得通过重做来解决哪个问题：忘记任务、不知道先做什么，还是看不清进度？
>
> 我建议先解决“不知道先做什么”，这样第一版有一个明确的用途。

**你**

> 不知道先做什么。只给我自己用，也不需要同步。其实可以做得很小。

**Grill Lite · 收尾**

> **建议：** 先做一个本地的每日优先级原型，再决定是否完整重做。
>
> **你已确定：** 个人使用、不需要同步、帮助选择下一项任务。
>
> **我采用的假设：** 第一版手动录入任务就够了。
>
> **下一步：** 在一张页面草图里放入任务收件箱和今日三项重点。

问到这里，已经足够给出方向，讨论就结束。

## 问得少，仍然问到点上

| 规则 | 带来的体验 |
| --- | --- |
| **每轮 1–2 题** | 一次只处理少量、能回答清楚的选择。 |
| **全程最多 5 题** | 整段讨论共用一个预算，追问也计入。 |
| **每题附建议和理由** | 有具体建议可以判断，不用从空白开始回答。 |
| **小选择采用默认值** | 可逆的细节交给助手，并清楚标明假设。 |
| **信息足够就收尾** | 能给结论就停，剩余题数不用凑满。 |

Grill Lite 聚焦会改变方向、范围或可行性的选择。关键假设仍然会被质疑，重要矛盾也会被指出。一句话里包含几个独立问题，就按几题计算。

## 节奏由你定

| 你说 | 助手就会 |
| --- | --- |
| `每轮一个问题，总共最多三个。` | 使用更小的提问预算。 |
| `重点看哪些地方可能让方案失败。` | 优先检查影响最大的风险。 |
| `先给结论。` | 立即收尾，给出建议和下一步。 |
| `过一下方案，然后直接实现。` | 讨论结束后，按你的授权继续执行。 |

上限不是配额。信息足够明确的方案可以**零追问**。需要更深入时，你也可以主动要求继续。

## 放进你正在用的助手

核心就是一份 [SKILL.md](SKILL.md)：纯 Markdown，不需要运行脚本、配置 API 密钥或依赖外部服务。支持 Agent Skills 格式的助手即可使用。Skills CLI 支持 Codex、Claude Code、Cursor 等助手，安装时选择你使用的工具。

技能规则使用英文，讨论会跟随你的语言；中文提问、中文收尾都可以。

<details>
<summary><strong>手动安装</strong></summary>

将 `SKILL.md` 和可选的 `agents/` 文件夹放到助手技能目录下的 `grill-lite` 文件夹。分发副本时保留 `LICENSE`。

Codex 的用户级路径之一为 `~/.agents/skills/grill-lite/`，详见[官方技能文档](https://learn.chatgpt.com/docs/build-skills)。

</details>

<details>
<summary><strong>提问上限如何计算</strong></summary>

预算覆盖整段讨论。每个需要独立回答的问题都计数，包括开场和确认问题。达到上限时，助手会在结论中列出仍然影响决策的关键缺口。

这个上限依靠模型遵循指令，并非程序强制计数。[人工行为检查场景](EVALS.md)覆盖问题计数、提前停止、自定义上限和执行边界，供评估使用，不代表已通过自动化行为测试。

</details>

## 一起把问题问得更准

欢迎提供一个小例子：哪次追问改变了你的决定，或者哪次已经可以收尾，助手却还在问。[提交 Issue](https://github.com/HUHANG716/grill-lite/issues)，也欢迎提出具体改进。

好的改进，应该让下一位使用者少一些不必要的来回，更快做出有依据的决定。

---

灵感来自 [Matt Pocock 的 grilling 技能](https://github.com/mattpocock/skills/blob/main/skills/productivity/grilling/SKILL.md)。规则独立编写，采用提问上限和明确的提前停止条件。

使用 [MIT 许可证](LICENSE)开源，欢迎使用、修改和分享。
