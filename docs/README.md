# Documentation Index — 文档地图

> `docs/` 的**唯一索引**。根 `README.md` 只回答"WAM 是什么"，这里回答"某个问题去哪找"。
> **`docs/` 只放 canonical**：已采纳、有状态标记的架构与契约。**某一条架构路径（Path）的东西不放这里**——它们住 [`../paths/`](../paths/)，晋升进来要走 `../PATH_GOVERNANCE.md` §5。
> 维护规则：新增或移动任何文档，必须同时改这张表。表与目录不一致 **≥2 次**，说明索引已失效——退回 README 单页地图。

---

## 1. 按"你想知道什么"找

| 你想知道 | 去读 | 什么时候读 |
|---|---|---|
| WAM 到底是什么、为什么存在 | [`vision.md`](vision.md) | 第一次接触；需要概念词汇时 |
| 人和 AI 怎么协作（四文件、六步、治理层） | [`foundation.md`](foundation.md) | 每一次会话开始 |
| 系统为什么长这样（循环、组件、边界、注意力状态机） | [`architecture.md`](architecture.md) | 要改设计、或质疑某个结构时 |
| 某个组件具体怎么工作、输入输出是什么 | [`specifications/`](specifications/) | 要实现它、或要验证它 |
| 某个结论有多硬（已确立 / 基线 / 假设 / 待定） | [`decisions/register.md`](decisions/register.md) | **引用任何结论之前** |
| 这周做什么、什么时候必须跑到哪 | [`development/roadmap.md`](development/roadmap.md) | 开工前 |
| 什么进 MVP、什么明确不进 | [`development/scope.md`](development/scope.md) | 想加需求时 |
| 工程怎么做（任务、阶段门、环境基线） | [`development/mvp-plan.md`](development/mvp-plan.md) | 写代码时 |
| 项目现在到哪一步了 | [`../workspace/state.md`](../workspace/state.md) | 每次会话开始；**不要在其他地方找** |
| 有别的整体架构在试吗、试到哪了 | [`../paths/`](../paths/) | 想开新路径、或怀疑 core 只是其中一条路径时 |

**三条阅读路径**

- **新贡献者**：`vision.md` → `decisions/register.md`（只看 C 类与 OQ）→ `development/scope.md` §4
- **要写代码**：`development/roadmap.md`（这周做什么）→ `specifications/execution-contract.md`（契约）→ `development/mvp-plan.md`（做法）
- **要判断某事算不算成立**：`decisions/register.md` → `specifications/acceptance.md` → 若涉及外部工作，见 [`../research/external-assets.md`](../research/external-assets.md)

---

## 2. 本目录的文件

| 文档 | 内容 | 状态 |
|---|---|---|
| [`foundation.md`](foundation.md) | M0 宪法：四文件状态模型 + 六步协议 + 三层治理（证据 / 提案 / 决策）与晋升门 | **in force**（被 `architecture.md` §2 局部修正，修正处已注明） |
| [`vision.md`](vision.md) | 问题定义（四重缺失 + 状态失同步）· 五核心概念 · 七条原则 · **WAM 没有自己的渴望** | current |
| [`architecture.md`](architecture.md) | 核心循环 · 组件职责 · 五级证据阶梯 · Persistent Record · 执行层边界 · Human Absent Mode · §12 注意力状态机（10 状态 / 6 模式） | current |
| [`specifications/state-and-evidence.md`](specifications/state-and-evidence.md) | Situation 必须表达什么 · 认识论五分 · Move 生命周期 · 跨会话恢复判据 | **specified**，无实现 |
| [`specifications/execution-contract.md`](specifications/execution-contract.md) | 6 个接口 · `.wam/state.json` 结构 · Move 状态机与幂等规则（原 `docs/06` §5–§7，节号保留） | **specified**，无实现 |
| [`specifications/acceptance.md`](specifications/acceptance.md) | 10 条行为验收（T1–T10）· 4 类设计验证场景（Kaggle / 论文复现 / 开源 / 社科） | **specified**，用例一条未跑 |
| [`decisions/register.md`](decisions/register.md) | 决策状态索引：13 已确立 · 17 基线 · 10 假设 · 27 开放问题 · **11 项文档与现实不一致** | current（引用必须带状态标记） |
| [`development/roadmap.md`](development/roadmap.md) | 九周 W0–W9 · 每周 E1 退出条件 · 三个决策 · 固定砍单顺序 · **W4 是唯一不可谈判的门** | **current plan**（时间的唯一权威） |
| [`development/scope.md`](development/scope.md) | 目标分类学 L×G×E · 36 格 · MVP 由格子推导（20 IN / 3 MIN / 1 SEAM / 12 OUT） | current（范围的唯一权威） |
| [`development/mvp-plan.md`](development/mvp-plan.md) | 环境基线 · A/B/C 能力分级 · 15 个任务 T-01→T-15 · 阶段门 · 批次计划（历史） · 自评 | current（工程做法），§12 已被 roadmap 取代 |
| [`development/dashboard-plan.md`](development/dashboard-plan.md) | 研发看板 P1–P4 | **deferred** — 九周内不做 |

---

## 3. 不在 `docs/` 的其他层

| 层 | 位置 | 一句话 |
|---|---|---|
| 起源 | [`../idea.md`](../idea.md) | 作者原文，一切主张的源头 |
| 知识 | [`../research/`](../research/) | 外部调研、外部资产核实、作者脑暴、原文汇编 |
| 外部论文库 | [`../reference/`](../reference/) | 要借鉴的论文 + 六阶段借鉴流程（入库→评估→提案→验证→整合→回访） |
| 架构路径 | [`../paths/`](../paths/) | 整套架构的探索 + 登记表；目前 1 条（`octsix`，Proposed）。规则见 [`../PATH_GOVERNANCE.md`](../PATH_GOVERNANCE.md) |
| 机制假设 | [`../directions/`](../directions/) | 单个机制/组件的提案；1 active / 4 parked / 1 archived |
| 跑过的验证 | [`../experiments/`](../experiments/) | 路径 = 一个局部结论；跑前 plan.md，跑后 results.md |
| 项目状态 | [`../workspace/`](../workspace/) | 局面 / 目标+证据 / 流水 / 决策事件。**唯一权威** |
| 对外页面 | [`../site/`](../site/) | 公开站；不承载任何实时状态 |

概念边界：`workspace/` 是**项目治理状态**（人和 AI 手写 Markdown）；**Shared Context** 是未来运行时的共享信息组织（由循环经 `StateRepository` 写）。两者名字相近，**但不是一个东西**——见 `architecture.md` 与 `directions/shared-context/`。

---

## 4. 一条规则

**同一类事实只允许有一个住处。** 发现第二处，删掉它，留一个指针。

| 事实 | 唯一住处 |
|---|---|
| 现在到哪一步、哪些未知 | `workspace/state.md` |
| 哪些目标完成、证据是什么 | `workspace/goals.md` |
| 做过什么（流水） | `workspace/log.md` |
| 决定过什么（事件 + 理由 + 替代方案） | `workspace/decisions.md` |
| 某个决定现在的状态 | `docs/decisions/register.md` |
| 这周做什么 | `docs/development/roadmap.md` |
| 做不做某功能 | `docs/development/scope.md` |
| 组件必须满足什么 | `docs/specifications/*` |
| 系统为什么这样设计 | `docs/architecture.md` |
| 协作规则 | `docs/foundation.md` |
