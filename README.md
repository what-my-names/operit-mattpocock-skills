# Matt Pocock Skills — Operit 中文版 v1.0.0

来自 [mattpocock/skills](https://github.com/mattpocock/skills)（作者 Matt Pocock，MIT License，原仓库 22 万+ star）的 Agent Skills 合集，已翻译为简体中文并适配 [Operit AI](https://operit.app)。

本仓库为正式版 v1.0.0，收录全部 **25 个稳定技能**（engineering 18 个 + productivity 7 个）。

## 这是什么

Matt Pocock 日常做真实工程使用的 agent skills 合集。它们不是"vibe coding"，而是一套从想法到交付的完整工程流程：盘问澄清 → 领域建模 → 拆分票证 → 测试驱动开发 → 代码审查 → 协作交接。

全部技能已翻译为简体中文，frontmatter（name、description）与 Markdown 结构保持原样，可直接被 Operit 识别加载。

## 技能清单（25 个）

### 规划（engineering）
| 技能 | 用途 |
|---|---|
| `grilling` / `grill-me` | 不断盘问用户的想法，压力测试计划或设计 |
| `grill-with-docs` | 边盘问边产出 ADR 和术语表 |
| `domain-modeling` | 构建项目领域模型，统一"黑话" |
| `codebase-design` | 设计深层模块的共享词汇，寻找深化机会 |
| `wayfinder` | 把一大块工作规划成问题跟踪器上的共享地图 |
| `improve-codebase-architecture` | 扫描代码库寻找架构深化机会，输出可视化报告 |

### 规格与票证
| 技能 | 用途 |
|---|---|
| `to-spec` | 把对话转化为规范并发布到问题跟踪器 |
| `to-tickets` | 把计划/规范拆成一组有依赖关系的子弹票 |
| `to-questionnaire` | 把没答完的决定变成问卷交给别人填 |
| `triage` | 用状态机转移 issue 和外部 PR |

### 研究与原型
| 技能 | 用途 |
|---|---|
| `research` | 基于高信任度一手来源调查问题，产出 Markdown 报告 |
| `prototype` | 构建一次性原型回答设计问题 |

### 实现
| 技能 | 用途 |
|---|---|
| `tdd` | 测试驱动开发（红-绿-重构） |
| `implement` | 根据规范或票证实施工作 |
| `code-review` | 沿标准轴 + 规格轴双轴审查改动 |
| `diagnosing-bugs` | 硬错误与性能回归的诊断循环 |
| `resolving-merge-conflicts` | 解决进行中的 git 合并/变基冲突 |
| `wizard` | 生成交互式 bash 向导，引导人类完成只有他们能做的步骤 |
| `setup-matt-pocock-skills` | 配置本套技能所需的问题跟踪器、标签和文档布局 |

### 协作与教学
| 技能 | 用途 |
|---|---|
| `handoff` | 把当前对话压缩成交接文档 |
| `teach` | 向用户传授新技能或概念 |
| `writing-for-agents` | 为 agent 撰写文档（AGENTS.md/技能） |
| `wait-what` | 停下，让上一句话重新讲清楚 |
| `ask-matt` | 技能路由器：根据情况推荐用哪个技能 |

## 在 Operit 中安装

### 方式一：本地复制

把 `skills/` 下需要的技能文件夹复制到：

```
/sdcard/Download/Operit/skills/
```

结构应为：

```
/sdcard/Download/Operit/skills/tdd/SKILL.md
/sdcard/Download/Operit/skills/code-review/SKILL.md
...
```

### 方式二：Operit 市场

Operit 市场的 Skill 类型条目以 GitHub 仓库为安装来源。本仓库根目录保持 `skills/<技能名>/SKILL.md` 布局，仓库地址即可直接作为 `repository_url` 安装。

## 技能边界说明（副作用披露）

本套技能面向真实工程仓库工作，按市场审核要求如实披露副作用范围：

- **外部网络**：`research` 的后台代理访问官方文档/API/网页等一手来源；`to-tickets`、`triage`、`wayfinder` 调用 GitHub/GitLab/Linear 等跟踪器 API；`diagnosing-bugs` 发起 curl/HTTP 调试请求并可重放网络捕获；`wizard` 打开第三方仪表板/网站 URL。
- **Shell/命令执行**：`wizard` 生成并执行交互式 bash 脚本；`diagnosing-bugs` 执行测试/CLI/浏览器脚本；`code-review` 执行只读 git diff/log；`resolving-merge-conflicts` 执行 git 命令直接修改仓库；`setup-matt-pocock-skills`、`tdd`、`implement`、`prototype`、`improve-codebase-architecture` 执行构建/测试/扫描命令。
- **仓库写入**：工程技能会按规范写入仓库文件——设计文档、规范与票证、代码与测试、交接文档、课程、AGENTS.md 等；`to-tickets`/`triage` 会在跟踪器创建/更新/关闭 issues 与 PR。
- **凭据与敏感数据**：`handoff` 的交接文档写入前先脱敏密钥/密码/个人信息；`diagnosing-bugs` 的调试产物与日志可能包含认证头、Cookie 等凭据，须先脱敏，且可能要求提供 HAR、日志、core dump 证据；`wizard` 会写入 `.env` 与 GitHub secrets（密文输入）；`gh`/`glab` 使用已认证的 CLI，认证不明文落盘。
- **人工确认边界**：所有高影响操作（创建/关闭 issue 与 PR、git 合并变基、发布、写 secrets、执行向导脚本）均需用户在对话中逐项确认后执行，无授权不自行实施。

## 版本

- **v1.0.0**（2026-08-18）：正式版。25 个稳定技能全部翻译润色完成，Markdown 结构完整，经 Operit 实测可加载。

## 版权与来源

- 上游项目：[mattpocock/skills](https://github.com/mattpocock/skills)，MIT License，版权归原作者 Matt Pocock
- 本项目为其中文翻译与 Operit 适配发行版，保留原 LICENSE 与作者版权声明
- 被技能引用的运行时资料（`docs/`、`CONTEXT.md`、`CLAUDE.md`/`AGENTS.md`）保留英文原文，避免破坏技能内交叉引用

## 适配说明

1. 目录扁平化：原仓库按分类嵌套（engineering/ productivity/ 等），已铺平为 `skills/<技能名>/`
2. 符号链接转实体文件：原 `AGENTS.md` 为符号链接，已改为实体副本
3. 未收录 in-progress（6 个）与 misc（4 个）技能：这些依赖原作者个人工具链或 Claude Code 专有能力，通用性弱
4. Claude 专用 frontmatter 字段（如 `disable-model-invocation`）Operit 会自动忽略，不影响加载
