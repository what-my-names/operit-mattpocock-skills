---
name: setup-matt-pocock-skills
description: 配置此存储库以获取工程技能 - 设置其问题跟踪器、triage 标签词汇和域文档布局。在首次使用其他工程技能之前运行一次。
disable-model-invocation: true
---

# 配置 Matt Pocock 的 Skills

搭好各工程技能所假设的每仓库配置：

- **问题跟踪器** — issue 存放的地方（默认 GitHub；开箱也支持本地 markdown）
- **分诊标签** — 五个规范分诊角色所用的标签字符串
- **领域文档** — `CONTEXT.md` 和 ADR 存在哪里，以及读取它们的消费规则

这是一个提示驱动的技能，不是确定性脚本。先探索，呈现你发现的东西，和用户确认，然后动手写。

## 流程

### 1. 探索

看看当前仓库，理解它的起始状态。读已存在的东西；不要假设：

- `git remote -v` 和 `.git/config` — 这是一个 GitHub 仓库吗？是哪一个？
- 仓库根部的 `AGENTS.md` 和 `CLAUDE.md` — 有哪个存在吗？其中是否已有 `## Agent skills` 小节？
- 仓库根部的 `CONTEXT.md` 和 `CONTEXT-MAP.md`
- `docs/adr/` 以及任何 `src/*/docs/adr/` 目录
- `docs/agents/` — 本技能先前的输出是否已经存在？
- `.scratch/` — 本地 markdown 问题跟踪器惯例已在使用的迹象
- `triage` 技能装了吗？（它是本技能旁边的同级 skill 文件夹，或在你可用技能列表里。）这决定 Section B 要不要跑。
- Monorepo 迹象 — `pnpm-workspace.yaml`、`package.json` 里的 `workspaces` 字段，或者带自己 `src/` 的 `packages/*`。只在真正的大型多包仓库里才呈现；没有它们就是单上下文，几乎所有仓库都如此。

### 2. 呈现发现并询问

总结哪些在、哪些缺。然后按顺序过每个 Section——一节、一个回答，再进下一节。

每节以推荐答案开头，让用户一句话就能接受。只有选择真正分叉时才给一行解释；探索已经敲定的事就整节跳过（`triage` 没装就跳过 Section B，没有 monorepo 就跳过 Section C）。

**Section A — 问题跟踪器。**

> 解释：问题跟踪器是这个仓库的 issue 存放地。`to-tickets`、`triage`、`to-spec` 这些技能要读写它——它们需要知道该调 `gh issue create`、在 `.scratch/` 下写 markdown 文件，还是按你描述的别的流程来。选择你实际跟踪这个仓库工作的地方。

默认姿态：这些技能是围绕 GitHub 设计的。`git remote` 指向 GitHub，就提议 GitHub。`git remote` 指向 GitLab（`gitlab.com` 或自托管主机），就提议 GitLab。否则（或用户有偏好），提供：

- **GitHub** — issue 住在这个仓库的 GitHub Issues（用 `gh` CLI）
- **GitLab** — issue 住在这个仓库的 GitLab Issues（用 [`glab`](https://gitlab.com/gitlab-org/cli) CLI）
- **本地 markdown** — issue 作为文件住在仓库的 `.scratch/<feature>/` 下（适合单人项目或没有远端的仓库）
- **其他**（Jira、Linear 等）— 请用户用一段话描述工作流；技能会以自由文本记录它

把选择记进 `docs/agents/issue-tracker.md`。GitHub 和 GitLab 模板带一个"PR 作为请求入口"开关，默认**关闭**——保持关闭、不要主动打开；想用外部 PR 的可以在文件里自己翻转。

**Section B — 分诊标签词汇。** 如果 `triage` 技能没装（探索已告诉你），整节跳过——没装的技能不需要标签。

装了的话，只问一个问题：

> 你想保留默认分诊标签吗？（推荐：**要**）

默认是五个规范角色，每个标签字符串等于名字：`needs-triage`、`needs-info`、`ready-for-agent`、`ready-for-human`、`wontfix`。回答**要**，就原样写入。只有用户说不要——通常因为他们的跟踪器已经用了别的名字（比如 `needs-triage` 对应 `bug:triage`）——才收集覆盖值，让 `triage` 应用已有标签而不是创建重复的。

**Section C — 领域文档。** 默认**单上下文**——仓库根部一个 `CONTEXT.md` + `docs/adr/`。这适合几乎所有仓库；不用问直接写。

只有在探索发现 monorepo 迹象时才提供**多上下文**——根部一个 `CONTEXT-MAP.md` 指向各上下文的 `CONTEXT.md`。然后确认他们要哪种布局。

### 3. 确认并编辑

给用户看一份草稿：

- 要加进正在编辑的 `CLAUDE.md` / `AGENTS.md`（选择规则见步骤 4）的 `## Agent skills` 块
- `docs/agents/issue-tracker.md`、`docs/agents/domain.md`、`docs/agents/triage-labels.md` 的内容（最后一个仅在 `triage` 已装时）

让他们先改，再写入。

### 4. 写入

**选择要编辑的文件：**

- `CLAUDE.md` 存在，编辑它。
- 否则 `AGENTS.md` 存在，编辑它。
- 都不存在，就问用户要创建哪个——不要替他们选。

`CLAUDE.md` 已存在时绝不创建 `AGENTS.md`（反之亦然）——永远编辑已有的那个。

选中的文件里如果已有 `## Agent skills` 块，就地更新内容，不要追加重复块。别覆盖用户对周边小节的改动。

块的内容：

```markdown
## Agent skills

### Issue tracker

[issue 跟踪位置的一行摘要]。见 `docs/agents/issue-tracker.md`。

### Triage labels

[标签词汇的一行摘要]。见 `docs/agents/triage-labels.md`。

### Domain docs

[布局的一行摘要——"单上下文"或"多上下文"]。见 `docs/agents/domain.md`。
```

只有当 `triage` 已装且 Section B 跑了，才包含 `### Triage labels` 子块并写 `docs/agents/triage-labels.md`。没跑的话两者都省略。

然后用本技能文件夹里的种子模板为起点写文档文件：

- [issue-tracker-github.md](./issue-tracker-github.md) — GitHub 问题跟踪器
- [issue-tracker-gitlab.md](./issue-tracker-gitlab.md) — GitLab 问题跟踪器
- [issue-tracker-local.md](./issue-tracker-local.md) — 本地 markdown 问题跟踪器
- [triage-labels.md](./triage-labels.md) — 标签映射（仅当 `triage` 已装）
- [domain.md](./domain.md) — 领域文档消费规则 + 布局

"其他"问题跟踪器则按用户的描述从零写 `docs/agents/issue-tracker.md`。

### 5. 完成

告诉用户配置完成，以及哪些工程技能现在会读这些文件。提一句他们以后可以直接编辑 `docs/agents/*.md`——只有想换问题跟踪器或从头再来时才需要重跑本技能。
