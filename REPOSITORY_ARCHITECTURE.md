# Repository Architecture — WAM Framework 仓库架构

> 日期：2026-11-10 · 状态：**提案（待 D-1 / D-2 / D-3 裁决后才进入 Phase 4）**
> 依据：[`REFACTORING_AUDIT.md`](REFACTORING_AUDIT.md) 的 13 条冲突、8 条结构问题、8 条迁移风险
> 目标不是"看起来专业"，是**同一类事实只有一个住处**，且这个住处能回答"它过期了谁负责改"。

---

## 0. 唯一的组织原则

> **目录 = 可信度 + 生命周期。不是写作顺序，不是文档类型。**

每份材料进仓库前只回答一个问题：**"它凭什么可以被人相信？"**

| 可信度 | 住哪 | 进来要满足 | 出去要满足 |
|---|---|---|---|
| 已起源/信念 | `idea.md` · `docs/vision.md` | 作者原文 | 永不出口 |
| 宪法 | `docs/foundation.md` | 作者确认的协作规则 | 只能被新版本替换，不被删 |
| 已采纳的设计 | `docs/architecture.md` · `docs/specifications/` · `docs/decisions/` | 有理由 + 有替代方案 + 有状态标记 | 过时 → 标 `superseded`，不删 |
| 计划与范围 | `docs/development/` | 有退出条件（E1） | 被新计划取代时整体降级为历史 |
| 外部知识 | `reference/`（要借鉴的）· `research/`（我们调研的） | 有出处 | 不移入规范层 |
| 未验证主张 | `directions/` | 一行假设 + 证伪条件 | 晋升 / parked / archive 三选一 |
| 跑过的验证 | `experiments/` | plan.md（跑前）+ results.md（跑后） | 结题即归档 |
| 项目自身状态 | `workspace/` | 有证据的"完成" | 只追加，不改写历史 |

因此：**`docs/` 里只放"我们现在就主张成立"的东西**；还不敢主张的，去 `directions/`。

---

## 1. 目标树

```text
WAM-Framework/
│
├── README.md                  入口：WAM 是什么 / 三条阅读路径 / 指针（不再复述状态）
├── CONTRIBUTING.md            新增：知识怎么组织、文档规则、晋升门、什么不算完成
├── .gitignore                 新增：.workbuddy/ · .wam/ · __pycache__/ · *.pyc
├── idea.md                    起源文本（不动）
│
├── docs/                      规范性层——"WAM 是什么、必须做什么"
│   ├── README.md              新增：唯一文档地图（README 只链到这里）
│   ├── foundation.md          ← docs/01  M0 宪法：四文件 + 六步 + 三层治理（现行）
│   ├── vision.md              ← docs/03  为什么 + 五概念 + 七原则 + "无自身渴望"
│   ├── architecture.md        ← docs/04  核心循环 / 组件协作 / 证据阶梯 / 执行边界 / §12 状态机
│   ├── specifications/        "组件具体怎么工作"——契约，可验证
│   │   ├── state-and-evidence.md   ← docs/05
│   │   ├── execution-contract.md   ← docs/06 §5–§7（接口 / state.json / Move 生命周期）
│   │   └── acceptance.md           ← docs/08
│   ├── decisions/
│   │   └── register.md        ← docs/07（事件流水仍在 workspace/decisions.md）
│   └── development/           计划与范围——"什么时候做什么"
│       ├── roadmap.md         ← docs/10  九周 W0–W9（时间的唯一权威）
│       ├── scope.md           ← docs/09  36 格 / MVP 推导（范围的唯一权威）
│       ├── mvp-plan.md        ← docs/06 剩余段（§1–§4, §8–§15）工程计划
│       └── dashboard-plan.md  ← docs/02  **deferred**（九周内不做，标注重开条件）
│
├── research/                  知识层——"外面知道的、我们抄回来的、作者写下的"
│   ├── README.md              新增：与 reference/ 的边界
│   ├── briefs/                ← docs/research/01–03（带 Sources 的调研简报）
│   ├── external-assets.md     ← docs/11（A/B/C 核实 + adopt/adapt/defer/reject）
│   ├── notes/                 ← rawnote.md（作者脑暴，5 张现场卡 + 14 个待吵）
│   └── archive/
│       └── raw-corpus.md      ← raw-archive.md（392 个文件原文汇编，3.5 MB）
│
├── directions/                提案层——"还没验证的主张"（名字与治理规则保留）
│   ├── README.md              治理：三层信任 + 晋升门（+ 新增 parked 出口）
│   ├── shared-context/        **active**（唯一活跃主张）
│   ├── global-route/          parked（内容已分流）
│   ├── substrate/             parked（第一刀 = roadmap W1）
│   ├── agent-plugin/          parked（与 shared-context 互斥，未裁决）
│   ├── weight-first/          parked（对 MVP 已拒绝，方向本身未证伪）
│   └── archive/architecture/  已取代（2026-08-07）
│
├── experiments/               执行层——"跑过的验证"
│   ├── README.md              宣言 + 生命周期 + DSH preset 机制
│   ├── _template/             路径模板（plan / results / artifacts / dsh）
│   └── archive/               结题路径
│
├── reference/                 外部论文库 + 借鉴流程（不动）
├── workspace/                 项目治理状态（宪法四文件，不动）
└── site/                      对外页面（路径不动）
```

**规模**：目标树 10 个实体目录，最深 3 层（`docs/specifications/*.md`）。当前 8 个实体目录，最深 3 层（`experiments/_template/stages/`）。**没有新增深度；新增文件只有 4 个**（`.gitignore`、`CONTRIBUTING.md`、`docs/README.md`、`research/README.md`）。

### 1.1 明确不建的目录（以及为什么）

| 参考方案里有 | 本仓现实 | 决定 |
|---|---|---|
| `src/wam/` · `tests/{unit,integration,acceptance}/` | **0 行实现代码**；`docs/10` W1 才建骨架，且 W1 窗口已过 | **不建。** 空目录不是架构，是给下一个人留下的"这里应该有东西"的假象。W1 的 T-01 建 `src/wam/` + `tests/`（`docs/06 §12.2` 已写产物） |
| `examples/` | 0 个用例；唯一计划中的验收对象叫 *fixture 项目*，且它本身是一个实验路径 | **不建。** 它出现时归 `experiments/`，因为它的用途是验证而非展示 |
| `scripts/` | 0 个脚本；唯一的脚本计划（dashboard）已推迟 | **不建。** 脚本出现时先问："它能被 `wam` CLI 取代吗"（`docs/02` P4 的答案正是"能"） |
| `docs/overview/` · `docs/architecture/` 两个子目录 | 实际正文 8 篇：overview 1 篇、architecture 1 篇 | **不建子目录。** 一个子目录装一个文件，是把层级当装饰 |
| `research/literature/` · `research/concepts/` · `research/_templates/` | 外部论文已有 `reference/`（含模板与六阶段流程），调研简报只有 3 篇 | **不建。** 重复的 literature 目录会让"这篇论文该放哪"变成两个答案 |
| `experiments/{active,completed,archived}/` | **0 条实验路径** | **不建。** 对 0 个元素做三分类，是把命名当进度。规则改为：路径住 `experiments/<id>/`，结题移 `experiments/archive/<id>/` |
| `LICENSE` | — | **不由本次添加。** 许可证是法律选择，不是结构选择，需作者决定 |

---

## 2. 每个目录的职责（放什么 / 不放什么 / 谁是权威）

| 目录 | 回答什么问题 | 该放 | 不该放 | 该类的**唯一权威** |
|---|---|---|---|---|
| 根 `README.md` | 这是什么、我该先读哪篇 | 定位、三条路径、指针 | 状态复述、进度、方向数 | — |
| `docs/foundation.md` | 人和 AI 怎么协作 | 协作规则、四文件、治理层 | 架构、计划 | 协作协议 |
| `docs/vision.md` | 为什么做、概念叫什么 | 问题定义、五概念、原则 | 实现细节、排期 | 术语与意图 |
| `docs/architecture.md` | 系统为什么长这样 | 循环、组件、边界、状态机、**设计理由** | 字段级 schema、任务清单 | 系统结构 |
| `docs/specifications/` | 组件怎么工作、怎么验 | 输入输出、数据结构、状态转换、验收判据 | 设计动机（指回 architecture）、排期 | **行为契约** |
| `docs/decisions/register.md` | 哪些结论有多硬 | C/B/H/OQ 四态 + 冲突台账 X | 决策发生的过程（在 workspace/） | **决策状态** |
| `docs/development/roadmap.md` | 这周做什么 | 周表、退出条件、砍单顺序 | 任务细节（在 mvp-plan） | **时间** |
| `docs/development/scope.md` | 什么进 MVP、什么不进 | 三轴格子、推导规则、类型声明 | 排期 | **范围** |
| `docs/development/mvp-plan.md` | 怎么造 | 环境基线、能力分级、任务、阶段门 | 周排期（指回 roadmap） | 工程做法 |
| `research/` | 我们知道了什么 | 简报、外部资产、作者原始材料、原文汇编 | 任何"我们主张"的结论 | **证据与外部分析** |
| `directions/` | 我们可能怎么做 | 假设、证伪条件、切片刻画 | 已采纳的设计、已跑的结论 | **未验证主张** |
| `experiments/` | 跑了什么、得到什么 | plan / results / artifacts / preset | 架构主张 | **实验结论** |
| `reference/` | 外面有什么可借 | 论文条目、评估矩阵、借鉴流程 | 我们的实验 | **外部文献** |
| `workspace/` | 项目现在到哪了 | 局面、目标+证据、流水、决策事件 | 设计文档 | **项目现状** |
| `site/` | 对外说什么 | 公开页 | 任何"实时状态"承诺 | — |

---

## 3. 一份新材料该放哪：判定顺序

按顺序问，第一个命中即停：

1. **是外部的东西吗？**（论文 / 别人的系统）→ `reference/`（要借鉴，走六阶段）或 `research/briefs/`（只做调研）。
2. **是我们还没证据的主张吗？** → `directions/<name>/`。**能写出证伪条件才准进。**
3. **是要跑的验证吗？** → `experiments/<id>/`，跑前有 `plan.md`，跑后有 `results.md`。
4. **是已经采纳、且会约束实现的决定吗？** → `docs/specifications/`（行为契约）或 `docs/decisions/register.md`（状态）+ `workspace/decisions.md`（事件）。
5. **是"什么时候做"吗？** → `docs/development/roadmap.md`。**是"做不做"吗？** → `docs/development/scope.md`。
6. **是"项目现在到哪了"吗？** → `workspace/`。**且只有这里。**

第 6 条是这次重构的核心：**README 不再有 §Status，site 不再有"实时状态"，docs 里任何一份文件都不再复述进度。**

---

## 4. Architecture 与 Specifications 的边界

判据一句话：**Architecture 回答"为什么"，Specification 回答"输入什么、输出什么、什么算通过"。**

| 问题 | 归属 | 本仓现状 |
|---|---|---|
| 为什么默认只有一个判断源？ | Architecture | `docs/04 §2`、`directions/shared-context §3` |
| `Judgment` 的字段有几个、`why` 必须引用什么？ | Specification | `docs/06 §5.2`（**错位**：混在 898 行计划里） |
| 状态怎么从 Proposed 走到 Committed？ | Specification | `docs/06 §7`（**错位**） |
| `.wam/state.json` 里有什么？ | Specification | `docs/06 §6`（**错位**） |
| 什么算"通过验收"？ | Specification | `docs/08`（**位置对，但混在 docs 根**） |
| 十个注意力状态为什么是十个？ | Architecture | `docs/04 §12`（位置正确） |
| MVP 收哪 20 个格子？ | 计划（不是规范） | `docs/09`（位置正确，但它不是架构也不是规范） |

**唯一的真错位是 `docs/06`**：它 898 行里同时装着环境基线、范围、**规范**、计划、自评。规范段（§5–§7）必须搬出去——不是为了好看，是因为**规范要稳定、计划要每周变**，两者同文件时，改计划就得动规范所在的文件（审计 P-08）。

### 4.1 规范的强制状态条

规则写在 `CONTRIBUTING.md`（规范怎么建、怎么标状态），因为它是"文档规则的唯一住处"。每份 `docs/specifications/*` 顶部必须有：

```markdown
> Status: specified | implemented | verified
> Version: <日期> · Supersedes: <无 / 路径>
> Carrier: <实现位置，或 "none — 无实现">
```

理由：本仓最贵的错误是"设计被读成实现"（`docs/06 §14` 自评第一条：*所有数据字段都是设计出来的，没跑过一次*）。状态条让这句话在每份规范的第一行可见，而不是藏在 898 行的第 870 行。

**默认值 `specified`。** 只有 `docs/07` 里能查到对应证据的，才允许写 `implemented` / `verified`。

---

## 5. 四层分离：Research / Experiments / Decisions / Specifications

| 层 | 问题 | 进层证据 | 出层方式 | 本仓现状 |
|---|---|---|---|---|
| **Research** | 外面/我们知道什么 | 有出处（URL / 论文 / 原文路径） | 不移出；过期加 `superseded` | 3 篇简报 + 11 + rawnote + raw-archive |
| **Experiment** | 这个假设成立吗 | `results.md` + 产物路径 + 失败项 | 结题 → `experiments/archive/` | **0 条** |
| **Direction** | 我们可能怎么走 | 一行假设 + 证伪条件 | promote / **parked** / archive | 1 active + 4 parked + 1 archived |
| **Decision** | 采纳了什么 | 理由 + 替代方案 + 权重判断 | 被新决策取代（不删） | 16 条事件 + 17 条基线 + 27 个开放问题 |
| **Specification** | 实现必须满足什么 | 输入输出 + 判据 + 状态条 | 随架构演进改版本 | 3 份（其中 1 份待拆出） |

**硬规则（写进 CONTRIBUTING）：**

1. **Research 里的话不能直接当 Decision 用。** 引用研究结论必须同时给出 `docs/07` 里的状态标记。
2. **Experiment 的结论是输入，不是决定**（`experiments/README` 宣言第 5 条，保留）。
3. **没有 `workspace/decisions.md` 事件 + `docs/decisions/register.md` 状态两条，就不算采纳。**
4. **Direction 的三个出口，第三个别漏**（见 §6.2）。

### 5.1 Evidence 的说法要能对上号

`docs/09` 已有 E1–E4 证据分级（可执行 / 可观察 / 外部判定 / 论证）。**规范状态条里的 `verified` 只对应 E1/E2**：一条命令能红绿，或一个可复现的观察。E3/E4 的结论只能标 `specified`。这条把 K-06 那类"35/36 格子"的抄错挡在源头上——数字必须能指回格子表。

---

## 6. `directions/` 的去留（审计 §5.1 的处置）

### 6.1 结论：**保留目录名，补一个状态出口**

保留的理由（不是惰性）：

- 这个名字写在**现行宪法** `docs/01 §Development Governance` 里，改它 = 改治理规则（审计 R-05，属需作者裁决项 D-1）。
- "拆分到 experiments / research / decisions"在本仓**会产生伪造归属**：4 个旧方向没有一个跑过实验（不能进 experiments）、不是外部知识（不是 research）、也没被采纳或被证伪（不是 decisions）。硬塞进去等于编造它们的历史。
- 它只有 1 active + 4 parked，目录开销接近 0；删掉再回来的成本更高。

### 6.2 补的出口：`parked`

现有晋升门只有 **promote** 与 **archive（= 验证失败）**。缺的这一格导致 4 个方向永久 `OPEN`（审计 P-06）。补：

```text
OPEN ──验证通过──> PROMOTED（进 docs/，目录移 archive/）
  │
  ├──验证失败──> ARCHIVED（记录失败原因）
  │
  └──暂无证据且暂不推进──> PARKED（写明：不解锁条件 + 谁在等什么）
```

`parked` 不是垃圾桶，是**诚实的第三种状态**：它必须写清"什么情况下会被重新打开"。四个方向的写法见迁移计划。

### 6.3 `shared-context` 的位置

它是唯一 active 的方向，且它的下一步是**一个实验**（`§6` 三阶段 DoD 已写死）。处置：**方向目录不动，实验开跑时在 `experiments/shared-context-scope-conflict/` 建路径，方向 README 的 Next step 指向它。** 不把方向本身搬进 experiments——因为方向还承载着 §3–§5 的理论主张（四个源、三层、三集合），那不是一次实验能装下的。

---

## 7. `workspace/` 的定位：两个 Workspace，不许合并

| | **Repository Workspace**（`workspace/`） | **Runtime Shared Context**（未来运行时） |
|---|---|---|
| 是什么 | 这个**项目**的状态：局面、目标、流水、决策 | WAM **运行时**里各执行实体共享的信息组织 |
| 谁写 | 人和 AI，直接改 Markdown | 循环本身，经 `StateRepository` 单写点 |
| 生命周期 | 永久，跨会话 | 单个项目的运行期，可重建 |
| 读者 | 下一次会话的人/AI | 判断源（Miracle Agent）与工具实体 |
| 失效方式 | 忘记更新 → 状态失真 | 多写者 → 状态失同步 |
| 权威文档 | `docs/foundation.md` | `docs/specifications/state-and-evidence.md` + `directions/shared-context/` |

**处置（也是 K-01 的安全解法）：**
1. 目录不改名（宪法条文，D-3）。
2. 运行时概念**一律写 `Shared Context` 全称**，禁止缩写成 "workspace"；`workspace/` 只指项目治理目录。
3. K-01（`workspace/*.md` vs `.wam/state.json`）**不在本次裁决**。重构只做一件事：让两个对象各有各的住处和名字，使这个冲突在文档结构上**可见**，而不是被目录名藏起来。

---

## 8. 文档依赖关系

```text
idea.md ──> docs/vision.md ──> docs/architecture.md ──> docs/specifications/*
                  │                    │                        │
                  │                    └──> docs/decisions/register.md
                  │                                             │
                  └──> docs/development/{scope,roadmap,mvp-plan} ┘
                                     │
workspace/state.md <─────────────────┘（只读：计划进度 → 现状）
workspace/goals.md ──证据──> docs/decisions/register.md
research/* ──> directions/* ──(实验)──> experiments/* ──> decisions
reference/* ──> research/*（借鉴入库 → 调研结论）
site/* <── 只从 README + docs/vision 取材（不抄状态）
```

| 文档 | 上游 | 下游（谁引用它） | 失效影响 |
|---|---|---|---|
| `docs/foundation.md` | idea.md | 全部（协议） | 协作规则失据 |
| `docs/architecture.md` | vision | specifications、directions | 规范失去理由 |
| `docs/specifications/*` | architecture、decisions | roadmap 的退出条件 | 无法判"做完了" |
| `docs/decisions/register.md` | workspace/decisions.md | 全部引用决策处 | 假设被当结论用 |
| `docs/development/roadmap.md` | scope、mvp-plan | workspace/state | 无时间基准（当前已发生） |
| `docs/development/scope.md` | decisions、taxonomy | roadmap、goals | 范围靠争论 |
| `workspace/*` | 全部 | 下一次会话 | **没人知道现在在哪** |

---

## 9. 生命周期规则

| 对象 | 生 | 变 | 死 |
|---|---|---|---|
| `docs/*` | 进 `docs/README.md` 索引 + 状态条 | 改内容不改位置；版本戳更新 | 被取代 → `Status: superseded by X`，**文件保留**（git 已是历史，仓库不再另设 archive） |
| `docs/specifications/*` | 状态条必填 | `specified → implemented → verified` 只能靠证据推进 | 随架构改版 |
| `directions/<name>` | 假设 + 证伪条件 + 权重 | work log 追加 | promote / parked / archive |
| `experiments/<id>` | 从 `_template/` 复制 | 每阶段 plan→results | 结题 → `archive/` |
| `research/*` | 有出处 | 追加新简报，不改旧结论 | 过时 → 标 `superseded`，不删 |
| `workspace/*` | 会话开始读、结束写 | 只追加，不改历史条目 | 永不删 |

**新增文档的准入（写进 CONTRIBUTING）：**

1. 能说清它属于 §5 的哪一层；说不清就不建。
2. 能在 `docs/README.md` 里占一行"它回答什么问题"。
3. **不新建与既有文档同题的文档**。同题 = 合并进既有文件（本次 `docs/06` 是反例，也是唯一要动刀的地方）。

---

## 10. 为什么不是参考方案的形状（逐条）

| 参考方案 | 采纳 | 理由 |
|---|---|---|
| `docs/{overview,architecture,specifications,decisions,development}/` 五子目录 | **部分**：只建后三个 | 8 篇正文摊进 5 个子目录 = 2 个目录各装 1 篇。**层级要由职责差异驱动，不由愿望驱动** |
| Architecture / Specifications 分离 | **完整采纳** | 这是本仓唯一真实存在的错位（`docs/06`），也是 P-08 的病灶 |
| Research / Experiments / Decisions 分离 | **采纳，但补齐第四层 Direction** | 参考方案把"未验证主张"落在 research 里，会让假设和研究混为一谈——这正是本仓 `directions/` 存在的理由 |
| `src/` `tests/` `examples/` `scripts/` | **不建** | 0 代码 / 0 脚本 / 0 用例。空目录会制造"已完成"的错觉 |
| `experiments/{active,completed,archived}` | **不建** | 0 条路径 |
| `workspace/{state,goals,log,decisions}.md` | **不动** | 已存在，且是宪法条文 |
| `research/literature` | **不建**（用 `reference/`） | 外部论文已有入库+评估+取舍的完整流程，再建一个 literature 会产生第二个答案 |
| `CONTRIBUTING.md` | **建** | 仓库组织规则必须有住处；否则规则只活在某次对话里 |
| `LICENSE` | **不建**（待作者定） | 法律选择，不是结构选择 |

---

## 11. 明确不做（防止这次重构自己过度设计）

- 不建空目录，不建占位 `.gitkeep` 层。
- 不拆 `docs/04`（它是合格的架构文档，577 行未到需要拆的规模；触发条件：>700 行或出现 2 个独立子系统 → 升为 `docs/architecture/` + 分册）。
- **不重排 `docs/06` 的章节**：整段搬家，保行号（`rawnote.md` 的 49 处 `文件:行号` 引用依赖这一点）。
- 不新建术语表、索引页、状态看板等**派生文档**——它们会立刻过期，而本仓的病灶就是派生文档。
- 不引入文档站点生成器、链接检查 CI（先人工跑一次脚本，稳定后再考虑）。
- 不动 `site/` 的设计与结构。

---

## 12. 这套结构怎么被推翻（写在前面，防止它变成新教条）

| 失效信号 | 说明 | 处置 |
|---|---|---|
| `docs/README.md` 与实际目录不一致 ≥2 次 | 索引没人维护 | 退回 README 单页地图，删 `docs/README.md` |
| `specifications/` 里出现"未实现却当已实现引用" | 状态条失效 | 加自动检查：`Status: implemented` 必须能在 `docs/07` 找到证据行 |
| `directions/parked/` 6 个月无人读、也无人解锁 | 这一层是惰性 | 全部移 `archive/`，删 parked |
| `research/` 与 `reference/` 出现同一篇论文 | 边界失效 | 合并，保留 `reference/` |
| 有人为了"结构完整"新建空目录 | 过度设计的复发 | 以本文 §1.1 为判据直接拒绝 |

---

## 13. 与当前结构的一句话对照

| 现在 | 之后 |
|---|---|
| 4 份"接下来做什么" | 1 份（`docs/development/roadmap.md`） |
| 4 份"现在到哪了" | 1 份（`workspace/state.md`），其余只放指针 |
| 3 处"有几个方向" | 0 处（方向以目录为准，README 不再计数） |
| 1 份 898 行的计划兼规范 | 规范 1 份 + 计划 1 份 |
| 2 份原始材料在根目录 | 1 个 `research/` 层，含原文汇编归档 |
| 4 个方向永久 `OPEN` | 1 active / 4 parked（各写解锁条件）/ 1 archived |
| 无 `.gitignore` | `.workbuddy/` 不进版本控制 |
