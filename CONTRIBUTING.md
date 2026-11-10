# Contributing — 往这个仓库里放东西的规矩

> 三条底线，其余都是它们的展开：
> **① 一类事实只有一个住处。② 没有证据不算完成。③ 没有证伪条件不算假设。**

---

## 1. 先判断它属于哪一层

| 层 | 位置 | 凭什么可以相信 | 出口 |
|---|---|---|---|
| 起源 / 信念 | `idea.md` · `docs/vision.md` | 作者原文 | 永不出口 |
| 宪法 | `docs/foundation.md` | 作者确认的协作规则 | 新版替换旧版，不删 |
| 规范 | `docs/architecture.md` · `docs/specifications/` | 有设计理由 + 有验收判据 + 有状态条 | 过时标 `superseded` |
| 决策 | `docs/decisions/register.md`（状态）· `workspace/decisions.md`（事件） | 理由 + 替代方案 + 权重判断 | 被新决策取代 |
| 计划 / 范围 | `docs/development/` | 有 E1 退出条件 | 被新计划取代 |
| 知识 | `research/`（我们的）· `reference/`（外部论文） | 有出处 | 不移入规范层 |
| 未验证主张 | `directions/<name>/` | 一行假设 + 证伪条件 | promote / parked / archive |
| 跑过的验证 | `experiments/<id>/` | plan.md + results.md + 产物 | 结题归档 |
| 项目状态 | `workspace/` | 有证据的"完成" | 只追加 |

## 2. 不知道该放哪：按顺序问，第一个命中即停

1. 是**外部的东西**（论文 / 别人的系统）？→ `reference/`（要借鉴）或 `research/briefs/`（只做调研）
2. 是**我们还没证据的主张**？→ `directions/`（写不出证伪条件就别放）
3. 是**要跑的验证**？→ `experiments/`
4. 是**已采纳、会约束实现的决定**？→ `docs/decisions/register.md` + `workspace/decisions.md`
5. 是"**什么时候做**"？→ `docs/development/roadmap.md`；是"**做不做**"？→ `docs/development/scope.md`
6. 是"**项目现在到哪了**"？→ `workspace/`。**且只有这里。**

## 3. 文档规则

- **每份 `docs/` 文档顶部必须有状态条**：`Status` / `Version` / `Carrier` / `Supersedes`。
- `Status` 只允许三个值：`specified`（设计已定，无实现）→ `implemented`（有承载）→ `verified`（E1/E2 证据）。**默认 `specified`。**
- 写 `implemented` / `verified` 必须能在 `docs/decisions/register.md` 里指到证据行；指不到就是 `specified`。
- **新增文档三条准入**：① 说清属于 §1 的哪一层；② 在 `docs/README.md` 里占一行"它回答什么问题"；③ **不与既有文档同题**。同题 = 合并进既有文件，不新建。
- **不建派生文档**：术语表、索引页、状态看板、周报。它们会立刻过期，而"派生文档过期"正是本仓库 2026-11-10 重构前的病灶。

## 4. 决策：两个文件都要写

| 文件 | 记什么 | 格式 |
|---|---|---|
| `workspace/decisions.md` | **事件**：什么时候决定了什么 | `- [日期] 决定 — 理由 — 替代方案 — 权重判断` |
| `docs/decisions/register.md` | **状态**：这个结论现在有多硬 | C（已确立）/ B（基线）/ H（假设）/ OQ（开放）/ X（文档与现实不一致） |

**只有两条都写了，才算采纳。** 引用任何结论时必须带状态标记——说"这是已确立的"和说"这是个假设"是两句完全不同的话。

## 5. 假设：三个出口，不许赖在 OPEN

`directions/<name>/README.md` 必须写：一行假设、权重档（critical path / enhancement / noise）、**证伪条件**、切片刻画。

结束方式只有三种：

- **PROMOTED** — 有决策 + 有证据 + 产物搬进 `docs/` 或代码树 + 目录移 `directions/archive/`
- **ARCHIVED** — 验证失败，记录失败原因。**只有这个出口可以宣称"这个方向错了"。**
- **PARKED** — 暂无证据且暂不推进。必须写：**什么条件下会被重新打开**、谁在等什么。

## 6. 实验：跑前写 DoD，跑后写证据

1. 从 `experiments/_template/` 复制为 `experiments/<path-id>/`
2. 每阶段：跑前 `plan.md`（做什么 + DoD + 时间盒），跑后 `results.md`（结果 + 产物路径 + 失败项，不隐藏）
3. 结论写进 `workspace/decisions.md`，目录移 `experiments/archive/`
4. **实验结论是输入，不是决定**——由作者做最终判断

## 7. 会话怎么开始、怎么收尾

- **开始**：读 `workspace/state.md` + `workspace/goals.md`（硬规则，见 `docs/foundation.md`）
- **结束**：写 `workspace/log.md`（一行也算），更新 `state.md` / `goals.md`
- **每一个"完成"必须带证据**：产物路径、命令输出、测试结果。无证据 = 未完成。
- 发现文档与现实不一致 → 记进 `docs/decisions/register.md` §5（X 表），**不要静默改掉原文**

## 8. 不做什么

- 不改写历史条目（`workspace/*` 只追加）
- 不修 `research/archive/raw-archive.md` 的内部链接（原文照录，33 处不可解析是正常的）
- 不建空目录、不建占位 `.gitkeep` 层（`src/` `tests/` 在 W1 真开工时再建）
- 不把未验证的设计写成已实现（状态条就是为此存在）
- 不同时维护两份同类事实——发现第二份，删掉它，留指针

## 9. 提交

- commit message 用英文，一次提交一件事
- **结构性移动用 `git mv`**（保留历史追踪）
- commit 前跑一遍链接检查（排除 `research/archive/raw-archive.md`）
