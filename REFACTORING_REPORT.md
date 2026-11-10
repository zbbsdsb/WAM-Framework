# Refactoring Report — 重构完成报告

> 日期：2026-11-10 · 范围：`main` 分支仓库结构 · 基线 commit：`03c0432`（重构前检查点）
> 执行 commit：`8f61edb`（docs + research）、`69d0083`（directions + workspace + README）
> 结论：**结构已落到"一类事实一个住处"；技术设计一条未改；W0/W1 的排期滑期是这次重构之外的事实，已如实登记。**

---

## 1. 迁移前后目录树

### 1.1 之前

```text
WAM-Framework/
├── README.md                ← 含 §Status（状态的 4 份拷贝之一）、12 行文档地图
├── idea.md
├── rawnote.md               ← 脑暴材料在根目录
├── raw-archive.md           ← 3.5 MB 原文汇编在根目录（全仓 96% 字节）
├── .gitattributes           （无 .gitignore）
├── docs/
│   ├── 01-foundation.md  02-dashboard-plan.md  03-vision-and-concepts.md
│   ├── 04-architecture.md  05-state-move-evidence.md  06-development-plan.md（898 行，兼规范与计划）
│   ├── 07-decision-register.md  08-scenarios-and-acceptance.md
│   ├── 09-goal-taxonomy.md  10-rd-roadmap-2027.md  11-external-assets.md
│   └── research/01–03.md    ← 证据层混在规范性目录里
├── directions/            ← 5 个方向全部 OPEN（4 个自 08-07 无动作）
├── experiments/           ← 路径空间（0 条路径）
├── reference/             ← 论文库 + 借鉴流程
├── site/                  ← index / details（details 含一份自称"镜像"的冻结快照）
└── workspace/             ← state / goals（三代计划并存）/ log / decisions
```

**问题密度**：42 篇 Markdown 里，4 份"接下来做什么"、4 份"现在到哪一步"、3 处"有几个方向"、3 处"几个格子"。

### 1.2 之后

```text
WAM-Framework/
├── README.md                    入口：WAM 是什么 + 4 条阅读路径 + 指针（不再复述状态）
├── CONTRIBUTING.md              内容归属规则：四层可信度 / 判定顺序 / 状态条 / 决策双文件 / 方向三出口
├── .gitignore                   .workbuddy/ · .wam/ · __pycache__
├── idea.md                      起源文本（未动）
│
├── docs/                        规范性层
│   ├── README.md                **唯一文档地图**
│   ├── foundation.md            ← 01（宪法，未改内容）
│   ├── vision.md                ← 03
│   ├── architecture.md          ← 04
│   ├── specifications/
│   │   ├── state-and-evidence.md    ← 05
│   │   ├── execution-contract.md    ← 06 §5–§7（原文搬迁，节号保留）
│   │   └── acceptance.md            ← 08
│   ├── decisions/register.md    ← 07
│   └── development/
│       ├── roadmap.md  ← 10      scope.md  ← 09
│       ├── mvp-plan.md ← 06 剩余（§0–§4 + §8–§15）
│       └── dashboard-plan.md    ← 02（标 deferred）
│
├── research/                    知识层
│   ├── README.md                与 reference/ 的边界
│   ├── briefs/01–03.md          ← docs/research/*
│   ├── external-assets.md       ← 11
│   ├── notes/rawnote.md         ← 根目录 rawnote.md
│   └── archive/raw-archive.md   ← 根目录 raw-archive.md（标 -diff）
│
├── directions/                  提案层（目录不动，加状态）
│   ├── README.md                晋升门新增第三出口 parked
│   ├── shared-context/          **ACTIVE**
│   ├── global-route/ substrate/ agent-plugin/ weight-first/   **PARKED**（各写解锁条件）
│   └── archive/architecture/    **ARCHIVED**
│
├── experiments/                 执行层（未动：0 条路径，不建空的三分布局）
├── reference/                   外部论文库（未动）
├── workspace/                   项目治理状态（未动位置；goals 去重）
└── site/                        对外页面（路径未动；状态区改标冻结快照）
```

文件数：51 → **59**（+4 报告、+3 规则/索引文档、+1 `.gitignore`）。

---

## 2. 迁移清单（逐条，含未执行项）

### 2.1 已执行

| Current Path | New Path | Action | Reason |
|---|---|---|---|
| `docs/01-foundation.md` | `docs/foundation.md` | RENAME | 宪法应在 docs 根，序号不代表层级 |
| `docs/03-vision-and-concepts.md` | `docs/vision.md` | RENAME | 名实一致 |
| `docs/04-architecture.md` | `docs/architecture.md` | RENAME | 架构的唯一住处；不拆（577 行未到拆的规模） |
| `docs/05-state-move-evidence.md` | `docs/specifications/state-and-evidence.md` | MOVE + 状态条 | 它已是规范，错在放在 docs 根 |
| `docs/08-scenarios-and-acceptance.md` | `docs/specifications/acceptance.md` | MOVE + 状态条 | 验收契约 |
| `docs/06-development-plan.md` §5–§7（232–549 行） | `docs/specifications/execution-contract.md` | **SPLIT** | 接口 / schema / Move 生命周期是契约，不是计划；**318 行原文照搬，§5/§6/§7 节号保留** |
| `docs/06-development-plan.md` 其余 | `docs/development/mvp-plan.md` | MOVE + 切口指针 | 工程做法；§12 批次段保留为历史 |
| `docs/07-decision-register.md` | `docs/decisions/register.md` | MOVE | 决策状态索引 |
| `docs/09-goal-taxonomy.md` | `docs/development/scope.md` | MOVE | 范围权威 |
| `docs/10-rd-roadmap-2027.md` | `docs/development/roadmap.md` | MOVE | 时间权威 |
| `docs/02-dashboard-plan.md` | `docs/development/dashboard-plan.md` | MOVE + 标 `deferred` | 九周内不做（roadmap §7） |
| `docs/11-external-assets.md` | `research/external-assets.md` | MOVE | 外部核实属知识层 |
| `docs/research/01–03` | `research/briefs/01–03` | MOVE | 证据层移出规范性目录 |
| `rawnote.md` | `research/notes/rawnote.md` | MOVE | 作者材料属知识层 |
| `raw-archive.md` | `research/archive/raw-archive.md` | MOVE + 修首行标题 | 原文汇编归档；`-diff` |
| `README.md` | `README.md` | **REWRITE** | 删 §Status（4 份之一）、删文档地图、"29 个跟踪文件"过期 |
| `workspace/goals.md` | 同左 | **REWRITE** | 三代计划（Stage 1–3 / MVP Phase 1–4 / 批次 0–4 / Dashboard P1–P4）移入"已作废"段并注明取代者；当前里程碑指向 roadmap/scope |
| `directions/README.md` | 同左 | REWRITE（治理段） | 晋升门加第三出口 `parked`；五个方向的状态与解锁条件列表 |
| `directions/*/README.md`（5 个 + 1 归档） | 同左 | KEEP + Status 头 | 4 parked（各写解锁条件）、1 active、1 archived |
| `site/details.html` | 同左 | 改一句 | §LIVE STATUS 不再自称"镜像"，改标 2026-08-07 冻结快照；`docs/research/` → `research/briefs/` |
| `workspace/{state,log,decisions}.md` | 同左 | 追加 | 协议要求 + 两处事实纠错（方向数 4→5、格子数 35→36） |
| `docs/decisions/register.md` | 同左 | 追加 | C-14（知识结构）、X-12（站点冻结快照）、X-13（格子数漂移） |
| — | `CONTRIBUTING.md` | CREATE | 内容归属规则必须有住处 |
| — | `docs/README.md` | CREATE | 唯一文档地图（取代 README 里的 12 行表格） |
| — | `research/README.md` | CREATE | `research/` 与 `reference/` 的边界 |
| — | `.gitignore` | CREATE | `.workbuddy/` 之前可被 `git add -A` 提交进公开仓库 |

### 2.2 MERGE 说明

**本次没有任何 MERGE。** 唯一可能被理解为合并的是 `workspace/goals.md`，但它是**去重而非合并**：作废条目全部保留在文末"已作废（历史，不删）"段，每条注明被谁取代，未删一行语义。

### 2.3 未执行（按判断拒绝，非遗漏）

| 计划/参考方案里的项 | 决定 | 理由 |
|---|---|---|
| `src/wam/` · `tests/` · `examples/` · `scripts/` | **不建** | 0 行代码、0 个用例、0 个脚本。空目录会制造"已完成"的错觉；W1 的 T-01 才建 `src/wam` + `tests` |
| `experiments/{active,completed,archived}/` | **不建** | 0 条实验路径。对 0 个元素做三分类是把命名当进度 |
| `research/literature/` `concepts/` | **不建** | 外部论文已有 `reference/`（含模板与六阶段流程），再建 literature 会产生第二个答案 |
| `docs/overview/` `docs/architecture/` 子目录 | **不建** | 8 篇正文摊进 5 个子目录会有 2 个各装 1 篇 |
| `LICENSE` | **未加** | 许可证是法律选择，不是结构选择，需作者定 |
| 拆 `docs/04` | **未拆** | 577 行未到拆的规模；触发条件（>700 行或 2 个独立子系统）写进架构文档 |
| 修 `raw-archive.md` 的 33 处内部链接 | **不修** | 原文照录，改了就不是原文 |
| 归档 4 个 parked 方向 | **未归档** | 它们没被验证也没被证伪；归档 = 伪造一次失败判定 |

---

## 3. 验证结果

| # | 检查 | 结果 |
|---|---|---|
| **V-1** | 全仓 Markdown 相对链接 | **0 处断链**（49 篇，排除 `research/archive/raw-archive.md` 的原文链接）。迁移前基线同为 0——没有引入新断链 |
| **V-2** | 旧路径残留 | **0 处**（排除四份重构报告，它们描述的是旧状态；另有一处 `directions/archive/architecture/README.md` 里 2026-08-07 的历史引用，属归档原文，按规则不改） |
| **V-3** | 拆分无内容丢失 | 把 `execution-contract.md`（去头部）+ `mvp-plan.md`（去注记）按原顺序拼接，与 `git show 03c0432:docs/06-development-plan.md` 比对：**694 个非空行，把路径 token 归一化后逐行相同**；剩下的 4 行差异全部是路径字符串（长路径改名、短写 `docs/05` 展开为全路径、链接目标 `10-rd-roadmap-2027.md` → `roadmap.md`）。**无一句正文改动** |
| **V-4** | `文件:行号` 引用 | `rawnote.md` 49 处：`docs/06` 的 12 处按新行号重算（§5–§7 段 `−223`，其余 `+1 / −315`，已抽验 3 处内容一致）；其余 37 处为纯改名，行号不变；4 处指向 README 的在文件头标注为"重构前行号" |
| **V-5** | 空目录 | **0 个**（`experiments/archive/` 有 `.gitkeep`） |
| **V-6** | 索引与目录一致 | `docs/` 实际 12 篇 = `docs/README.md` + 表中 11 篇，一一对应 |
| **V-7** | 状态复述 | `README.md` 中 `M1/M2/M3/W4/Current stage` 出现 **0 次**（只有指针）；`site/details.html` 的 "mirror" 只剩否定句 "not a live mirror" |

两条补充核对：

- **格子数**：`scope` §1 与 §4.2 为 `36 = 7+5+7+7+6+4`，四个集合 `20 + 3 + 1 + 12 = 36`。此前 `README` / `state.md` / `goals.md` 的"35"是漏了 `MVP-SEAM` 一类，已改。
- **方向数**：`state.md` / `dashboard-plan.md` / `site/details.html` 的"4 个方向"已改或已标冻结；`README` 不再计数。

---

## 4. 遗留问题

### 4.1 需要作者动手（不是我能代替的）

| # | 事项 | 为什么必须由作者做 |
|---|---|---|
| **L-1** | **`site/details.html` 已改，但 `gh-pages` 分支未同步** | 无 GitHub 凭据，`git push` 不可用。线上仍是旧表述（"如实镜像"）。同步方式见 `workspace/log.md` 2026-08-07 的部署教训（`git show main:site/details.html` → 落到 gh-pages 根） |
| **L-2** | 四份重构报告暂在根目录 | 评审后建议移入 `research/archive/refactor-2026-11/`（`git mv`）。现在放根目录是为了你打开方便；已登记为待办，不藏 |
| **L-3** | `LICENSE` 未定 | 法律选择 |
| **L-4** | 三个 commit 未推送 | 无凭证；`03c0432` / `8f61edb` / `69d0083` 在本地 `main` |

### 4.2 有意未解决的冲突（重构不裁决设计）

| # | 冲突 | 现状 |
|---|---|---|
| **K-01** | `workspace/*.md`（宪法说它是状态权威）vs `.wam/state.json`（MVP 说它是循环权威） | **仍开着**（B-13 / OQ-18）。本次只做到让两个对象各有各的名字与住处：`workspace/` = 项目治理状态；`Shared Context` = 运行时，全称书写，不缩写为 workspace |
| **K-09** | 六步循环（宪法原文）vs `architecture` §2 的三处修正 | 宪法保留原文，修正指针保留。**未合并成一份新宪法**——那是设计决策，不是结构决策 |
| **OQ-09 / OQ-10** | WAM 与 Sponge 的关系；是否绑定执行平台 | 仍开着；`directions/global-route` 与 `agent-plugin` 里的 Hermes 表述保留原文 + 过期标注 |
| **K-02 / K-03** | `mvp-plan` §1.2 仍写 codex 为第一执行器；P0-1 在待办里显示未完成 | 正文保留历史版本（不静默改写），`§12` 注记 + `register` B-15/X-10 为准；`goals.md` 里 P0-1 已移入"已作废"并写明证伪 |

### 4.3 这次重构没能解决的那件事

`docs/development/roadmap.md` 的 W0（10-28→11-01）和 W1（11-02→11-08）**都已关闭，仓内 0 个 `.py` 文件**。这正是 `roadmap` §5 写的 S-1 早期信号（"又变成写文档"），而本次重构又是一次纯文档会话——第 5 次。

重构能让下一次会话不再花时间判断"哪份文件是对的"（`rawnote.md` §4 整节在做这件事），但它不会让代码出现。**W2 的窗口是 11-09→11-15，今天是 11-10。**

---

## 5. 回滚

| 想回到 | 命令 |
|---|---|
| 重构前（保留所有内容） | `git reset --hard 03c0432`（**会丢未提交改动，先确认工作树干净**） |
| 只撤销某一批 | `git revert 69d0083`（directions/workspace/README）或 `git revert 8f61edb`（docs/research） |
| 只撤销 `docs/06` 拆分 | `git show 03c0432:docs/06-development-plan.md` 可取回原文件，两份新文件可删 |

不建议 `--amend` 或 `push --force`：三个 commit 各自可独立回滚，历史比整洁更有用。

---

## 6. 补充（2026-11-11）：多路径架构支持

作者补充要求：WAM 必须支持多条独立的**架构路径**（`OctSix` 是当前一条），仓库不能围绕任何单一路径设计。

### 6.1 上一版漏在哪

上一版的判据是"同一事实是否有多份拷贝"。这一层缺失不是拷贝问题，是**坐标系问题**：目标树默认了"仓库 = 一套架构 + 若干提案"。于是：

- 第二条架构无处安放——写进 `docs/` 等于宣称已采纳（违反 No false finality），写进 `directions/` 等于把架构降格成机制提案。
- `OctSix` 在仓库里**零内容**：全仓只有 `research/archive/raw-archive.md` B-288 的一份 334 B 空 canvas（节点"未命名组 / Ori Agent"）。

### 6.2 做了什么

| 产出 | 内容 |
|---|---|
| `PATH_GOVERNANCE.md` | Path 定义（9 项，只有"架构假设"是必需）· 三层知识（路径内 / 跨路径 / canonical）· 目录规则 · 生命周期（Proposed→Exploring→Validating→{Promoted\|Paused\|Archived}）· **组件级**晋升规则 · 11 维度比较 · Path vs Direction vs Core · 8 条可检查禁令 · 这一层自己的失效条件 |
| `paths/README.md` | 登记表（6 列，1 行）+ 加一条新路径的 5 步（判据：新增不改任何既有文件） |
| `paths/_template/` | `README.md` / `hypothesis.md` / `comparison.md` —— 三份都是空骨架，不是范例 |
| `paths/octsix/README.md` | 状态 **Proposed**；作者口述的六空间照录；与 `docs/` 的**词面**对照（明确声明"不是等价判断"）；与 `directions/shared-context` 的分层说明；OQ-28；下一步 |
| 规则接线 | `CONTRIBUTING.md` 判定顺序加第 0 问；`docs/README.md` 声明 canonical-only；`README.md` 加一条路径与一段说明；`experiments/README.md` 加 `path:` 归属字段 |
| 台账 | `docs/decisions/register.md` C-15 + OQ-28；`workspace/` 四文件各一条 |

### 6.3 三条关键取舍

1. **建层，不填内容。** 六个空间只有名字，没有假设、边界、判据。给它们建 `architecture/` 就是在用目录假装进度。`paths/octsix/` 因此只有 1 个文件。
2. **`directions/` 降为机制层，不合并进 `paths/`。** 五条方向都是"可插进任何架构的机制"（共享上下文、状态基板、目标 DAG…），与"整套架构"不同层。合并会毁掉唯一能产生对比的那个区分。
3. **实验不复制进 Path。** 实验住顶层 `experiments/<id>/`，README 写 `path:` 字段。复制 = 第二真相；锁进路径目录 = 结果无法被别的路径读到。

### 6.4 没有照搬参考方案的两处

- **不改 `docs/` → `core/`**：`core/` 会与未来 `src/wam/core` 代码树撞名；`docs/` 在本仓已被定义为"已采纳"；规则要的是"`docs/` 只放 canonical"，不是"它必须叫 core"。映射已备好，要改是一条 `git mv`。
- **不建 `research/{shared,literature}`**：`reference/` 已经是 literature（有入库/评估/六阶段流程）。

### 6.5 验证

| # | 检查 | 结果 |
|---|---|---|
| V-8 | 登记表行数 = 实际路径数 | 1 = 1 |
| V-9 | `paths/octsix/` 文件数 | **1**（只有 README） |
| V-10 | `docs/` 被污染程度 | 仅 `register.md` + `README.md`；其余 10 篇零改动 |
| V-11 | `octsix` 在 `docs/` 的出现 | **正文（architecture / vision / foundation / specifications / development）0 处**；仅在 `decisions/register.md`（2 行，C-15 与 OQ-28 的登记）与 `docs/README.md`（1 行，索引）出现——登记需要，不是架构采用 |
| V-12 | 全仓链接 | 0 断链 |

### 6.6 需要作者裁决

**OQ-28：`docs/` 现在的内容，是 canonical WAM，还是 OctSix 的早期形态？**

作者的话（"不能因为它们在当前路径里就变成 WAM 的强制顶层抽象"）指向后者；register 里 B 类登记指向前者。**本次按前者处理**，因为那是可逆的一边——把文件搬进 `paths/octsix/` 随时可做；把 canonical 降级后，所有引用"已采纳"的地方都会失效。

若答案是后者，预置动作写在 `REPOSITORY_MIGRATION_PLAN.md` §12.3（4 步，其中第 3 步需要作者重写 `docs/vision.md`，不是搬家能完成的）。
