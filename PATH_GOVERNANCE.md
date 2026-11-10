# Path Governance — 架构路径的治理

> 一句话：**Path 是"一整套架构假设"，不是"一个功能提案"。仓库必须能同时容纳多个 Path，且没有任何一个 Path 是默认的那一个。**
> 上位：`docs/foundation.md`（三层信任 + 晋升门）· 同级：`directions/README.md`（机制级提案）· 登记表：[`paths/README.md`](paths/README.md)

---

## 0. 为什么必须单独有一层

2026-11-10 的重构解决了"同一事实多份拷贝"，但**它默认了仓库只有一条架构**：`docs/architecture.md` + `docs/specifications/*` + 一份 `mvp-plan`。

后果是可验证的：

- `OctSix` —— 作者当前在用的架构探索名 —— 在仓库里**只存在于一份空 canvas**（`research/archive/raw-archive.md` B-288，节点仅 "未命名组 / Ori Agent"）。它的六个候选空间没有一个字被写下来。
- 第二条路径若出现，**没有地方可放**：写进 `docs/` 就等于宣称它是 canonical（违反 No false finality），写进 `directions/` 又太轻（那是机制级假设，见 §7）。
- 一份 `docs/architecture.md` 同时承担"我们主张的架构"和"我们在试的架构"，**一旦要写第二条，只能改写第一条**——历史被覆盖，对比消失。

所以这一层的存在理由不是分类洁癖，而是：**没有它，第二个架构只能以覆盖第一个为代价出现。**

---

## 1. 什么是 Path

Path = 一条**独立的架构探索**。它自带以下九项中的任意子集，但必须能说清"**与 core 的差异在哪**"：

| # | 项 | 必须？ | 说明 |
|---|---|---|---|
| 1 | 架构假设 | **是** | 一句话：这套架构认为问题出在哪、靠什么解决 |
| 2 | 概念模型 | 建议 | 它自己的核心名词与边界（例：OctSix 的六个空间） |
| 3 | 组件分类 | 建议 | 有哪些部件、各自负责什么 |
| 4 | 交互 / 协调机制 | 建议 | 谁跟谁说话、怎么仲裁 |
| 5 | 执行模型 | 建议 | 一次执行怎么开始、怎么结束、怎么中断 |
| 6 | 状态表示 | 建议 | 状态存什么、存哪、谁写 |
| 7 | 研究问题 | 建议 | 它想回答但还不知道答案的问题 |
| 8 | 实验与验证判据 | 建议 | 什么结果会让它被削弱 |
| 9 | 技术实现路线 | 可选 | 语言、运行时、依赖 |

**Path 可以不完整。** 不完整不是缺陷——`Proposed` 状态就是用来装不完整的。但**没有第 1 项的 Path 不许建立**：只有名字不构成假设。

---

## 2. 三层知识（这是本文件最重要的一张表）

| 层 | 是什么 | 住哪 | 能进下一步的条件 |
|---|---|---|---|
| **A. 路径内** | 只对一条 Path 成立的：它的概念模型、图、组件定义、路径内假设、路径内实验 | `paths/<id>/` | 晋升到 core 需要**显式决定 + 证据**（§5） |
| **B. 跨路径** | 可能对多条 Path 有用的：调研、外部工作、机制研究（如 Shared Context 研究、认知模型、状态表示、调度、可验证执行） | `research/`（我们的）· `reference/`（外部论文） | 不自动变成架构。**共享研究 ≠ 共享架构** |
| **C. Canonical** | 已被显式采纳、作为共同 WAM 架构的一部分 | `docs/` + `workspace/decisions.md` + `docs/decisions/register.md` | 只能靠 §5 的晋升进入 |

**硬规则（对应指令 §3C）**：**一个概念在多条 Path 里都出现，不构成晋升证据。** 三条路径都用"Shared Context"这个名字，只能说明这个词好用，不能说明它属于 canonical WAM。晋升需要一次显式决定 + 一条可检查的证据。

---

## 3. 目录

```text
paths/
├── README.md              登记表（Registry）+ 怎么加一条新 Path
├── _template/             最小模板：README / hypothesis / comparison
└── octsix/                当前唯一登记的 Path（内容尚未写，见其 README）
```

单条 Path 内部**按需建立**子目录，不预建空的：

```text
paths/<id>/
├── README.md              必需：这是什么、状态、与 core 和其他 Path 的关系
├── hypothesis.md          必需：一行假设 + 证伪条件 + 什么算晋升
├── comparison.md          建议：跨路径比较（§6），允许写"未建模"
├── architecture.md        可选：它自己的结构（可以拆成 architecture/ 目录）
├── specifications/        可选：它自己的契约——**只在它真的需要时**
└── decisions.md           可选：路径内决定（**不进** core 的 register）
```

**不做的事**：每条 Path 里不放 `research/`、`experiments/` 的副本。

- 跨路径知识 → 链到 `research/`，不复制（复制 = 两份真相 = 回到 2026-11-10 的病）。
- 实验 → 一律住顶层 `experiments/<id>/`，README 里用一行 `path: <id>` 声明归属。理由：实验结果的价值在于**可被别的 Path 读到**，把它锁在路径目录里就失去了对比意义（指令 §4 的"shared experiments 应该分开存吗"——答案是"是"，但共享层就是顶层那一层，不是每条路径各建一份）。

---

## 4. 生命周期

```text
Proposed ──> Exploring ──> Validating ──┬──> Promoted
    │            │              │        ├──> Paused ──> Resumed
    │            │              │        └──> Archived
    └────────────┴──────────────┴───────────> Archived（放弃，保留历史）
```

| 状态 | 判据 | 允许的下一步 |
|---|---|---|
| **Proposed** | 有名字 + 一行假设，什么都没有 | Exploring / Archived |
| **Exploring** | 在写它的概念模型或结构；**不要求**任何证据 | Validating / Paused / Archived |
| **Validating** | 有明确的验证判据，且至少一个实验在跑或有结果 | Promoted / Paused / Archived |
| **Paused** | 暂不推进，**必须写"什么条件下恢复"** | Resumed / Archived |
| **Promoted** | 已被采纳为 canonical（可能是部分组件） | 保留目录；记 promoted 日期与范围 |
| **Archived** | 主动放弃或被证伪，**必须写原因** | 不可复活（要复活就建新 Path 并引用旧的） |

三条松弛（对应指令 §5）：

1. **可以长期停在 Exploring。** 没有时间上限，也没有"该出结果了"的默认压力。
2. **Promoted 不等于整条 Path 通过。** 状态是路径级的，但晋升是**组件级**的（§5），所以状态写 `Promoted (partial: <组件列表>)`。
3. **Paused 不许没有解锁条件。** 写不出解锁条件的，就是 Archived 而不是 Paused（同 `directions/` 的规则）。

---

## 5. 晋升规则

### 5.1 组件级晋升（常态）

一条 Path 的某个部件进入 canonical，需要**全部**满足：

1. 一条决定：`workspace/decisions.md` 记事件 + `docs/decisions/register.md` 记状态（C 或 B 类）；
2. 一条证据：E1（一条命令能红绿）或 E2（可复现的观察）。E3/E4 不够；
3. 文本搬运：写进 `docs/architecture.md` / `docs/specifications/`，并**标注来源**（`origin: paths/<id>`）；
4. 原 Path 的记录：`paths/<id>/README.md` 的"已晋升组件"加一行，**原文件不删**。

### 5.2 整条 Path 晋升（罕见）

只有当这条 Path 的架构**就是** canonical 架构时：

1. `docs/architecture.md` 被重写（旧版本标 `superseded by paths/<id>`，不删）；
2. register 记一条 C 类；
3. `paths/<id>/README.md` 状态改 `Promoted`，路径目录**保留**——它是"为什么变成这样"的唯一记录。

### 5.3 不许做的事

- 因为"两条路径都这么说"就晋升（§2 硬规则）。
- 因为"实现起来方便"就晋升（那是实现细节，不是架构采纳）。
- 把 Path 的目录整体拷进 `docs/`（那是覆盖，不是晋升）。

---

## 6. 跨路径比较

比较放 `paths/<id>/comparison.md`，维度如下。**每条 Path 可以写"未建模"或"刻意不同：…"，不许为了对齐而编答案。**

| # | 维度 | 写法要求 |
|---|---|---|
| 1 | 核心架构假设 | 一句话，必须能与 core 的假设对照 |
| 2 | 智能主体的模型 | 一个？多个？谁做判断？ |
| 3 | 上下文管理 | 信息怎么组织、谁能看、边界在哪 |
| 4 | 认知与推理 | 判断怎么形成，是否显式比较候选 |
| 5 | 规划与执行 | 谁生成步骤、谁执行、怎么中断 |
| 6 | 状态与记忆 | 存什么、谁写、怎么恢复 |
| 7 | 反思与反馈 | 失败怎么变成下一次的输入 |
| 8 | 可扩展性 | 加一个能力要改哪里 |
| 9 | 验证策略 | 什么算"这个架构成立" |
| 10 | 实现复杂度 | 最少要写多少东西才能跑一次 |
| 11 | 未解问题 | 它自己承认不知道的 |

**登记表不存这些答案。** `paths/README.md` 只存"哪条路径声称回答了哪些维度"的指针——把 11 个维度做成登记表的列，就是在强迫所有 Path 用同一套分类，正是指令 §6 禁止的。

---

## 7. Path / Direction / Core 三者的区别

这是最容易混的一处，单独写死：

| | Path（`paths/`） | Direction（`directions/`） | Core（`docs/`） |
|---|---|---|---|
| 粒度 | **整套架构**：有自己的概念模型 | **一个机制 / 组件**：可插进任何架构 | 已采纳的架构与契约 |
| 典型问句 | "WAM 应该由哪几个空间构成？" | "状态该不该用单一写点？" | "现在必须遵守什么？" |
| 例子 | OctSix 的六个空间 | 分层共享上下文、状态基板 CLI、目标 DAG | 核心循环、6 个接口、Move 生命周期 |
| 可信度 | 提案（未验证） | 提案（未验证） | 已采纳（有状态标记） |
| 出口 | Promoted / Paused / Archived | promote / parked / archive | superseded |

**同名不同层是允许的，合并是禁止的**（指令 §7.6）。当前就有一例：

> **OctSix 的 `Shared Context` 空间** ≠ **`directions/shared-context` 机制方向** ≠ **`docs/` 的 `Situation` 概念**。

三者字面相近，层不同。书写时必须带限定："OctSix 的 Shared Context 空间"、"shared-context 机制方向"。**看到同一个词就合并，等于用词表代替架构。**

---

## 8. 禁止事项（指令 §7 的可检查版本）

| # | 禁止 | 怎么检查 |
|---|---|---|
| 1 | 不要围绕 OctSix 设计整个仓库 | `docs/` 里不出现 `octsix` 专有名词（除来源标注）；`paths/octsix/` 之外不引用它的六个空间 |
| 2 | 不要假设 WAM 永远有六个空间 | `docs/` 不写"六个空间"；`docs/architecture.md` 不引入 `Cognition`/`Reflection` 作为顶层概念 |
| 3 | 不要假设未来 Path 共享 OctSix 的概念模型 | 新 Path 的 README 必须有自己的概念模型段，哪怕只有三行 |
| 4 | 不自动把路径概念提升为 canonical | 晋升必须能在 register 里指到一条 C/B 记录 + 一条 E1/E2 证据 |
| 5 | 不重复共享研究 | 同一份调研出现两次 → 留 `research/`，另一处只留指针 |
| 6 | 不因为术语相似就合并 Path | 合并需要一条 decision，写清"为什么不是两个" |
| 7 | 保留每条 Path 的独立演化与历史 | Path 目录只追加不删；Archived 也不删 |
| 8 | 加一条新 Path 不需要重构仓库 | 判据：新增 = 一个目录 + 登记表一行 + 不修改任何既有文件 |

---

## 9. 这套治理怎么被推翻

写在前面，防止它变成新的教条：

| 信号 | 说明 | 处置 |
|---|---|---|
| `paths/` 长期只有 1 条 Path，且 6 个月没有新条目 | "多路径"是想象，不是需求 | 退化为 `paths/` 单目录（无 registry），或把 octsix 并入 `docs/` 并承认单架构 |
| `comparison.md` 从未被填写 | 比较框架是装饰 | 删除该文件要求，只留 README 的一行"与 core 的差异" |
| 晋升规则从未被执行（0 次组件晋升） | 规则只是文本 | 简化成"作者说采纳就采纳，但要写一条 decision" |
| 出现 3 条以上 Path 且互相引用混乱 | 层不够用 | 才考虑加"路径族 / Path family"，现在不加 |
