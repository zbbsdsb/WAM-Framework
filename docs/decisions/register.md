# Decision Register — 决策登记表

> 版本：2026-10-09 · **本文档是当前设计状态的唯一权威索引。**
>
> **与 `workspace/decisions.md` 的分工**：
> - `workspace/decisions.md` = **时间线日志**（按日期追加，记录"当时做了什么决定、理由、替代方案"），是 M0 已交付的地基，不改格式。
> - 本文档 = **状态索引**（按四态归类，回答"现在哪些是真的、哪些还没定"）。
>
> 新增决策时**两处都要写**：日志记事件，本表记状态。

---

## 0. 四种状态

| 状态 | 含义 | 能否作为开发依据 |
|---|---|---|
| **Confirmed / Established 已确立** | 项目愿景、核心问题、已明确提出的设计约束 | ✅ 可以 |
| **Current Design Baseline 当前设计基线** | 已收敛、适合用来继续设计和规划 MVP 的方向 | ✅ 可以，但标明"仍需与现有代码和实际约束对齐" |
| **Working Hypothesis 待验证假设** | 有吸引力但尚未证明必要或正确的方案 | ❌ **不可直接实现**，需先验证 |
| **Open Question 开放问题** | 仍影响设计或正式开发、需通过研究或实验解决 | ❌ 必须先裁决 |

**禁止把 Working Hypothesis 或 Open Question 写成 Confirmed Decision。** 本文档存在的首要目的就是防止这件事发生。

---

## 1. Confirmed / Established 已确立

### C-01 WAM 面向长周期、高复杂度项目

- **内容**：WAM 面向的不是一问一答，是需要持续推进的复杂项目。
- **来源**：`idea.md`；`README.md`
- **性质**：项目愿景。不可被后续实现困难推翻，只能被重新定义愿景。

### C-02 WAM 不应被限定为一问一答

- **内容**：框架的核心主张是"在对话之外继续有效"。
- **来源**：`idea.md` 四重缺失；`README.md` §The Problem
- **性质**：对框架形态的硬约束。任何把 WAM 实现为"更好的问答接口"的方案直接违反本条。

### C-03 核心问题诊断：四重缺失 + 状态失同步

- **内容**：Constructiveness / Continuity / Verifiability / Weight judgment 四重缺失，根因是 state desync。
- **来源**：`idea.md`
- **性质**：问题定义。已被 `research/briefs/01-ecosystem-survey.md` 独立佐证（行业普遍缺失可读共享状态与验证机制）。

### C-04 WAM 本身没有独立的内在渴望

- **内容**：WAM 围绕用户明确或授权的意图工作。自主判断服务于用户意图、既定原则、约束与授权范围，不服务于 WAM 自己的目标。
- **来源**：`docs/vision.md` §3
- **性质**：**本项目最重要的架构前提。** 直接推出两条硬规则：
  1. 不设计必须靠单一 Reward Function / Priority Score / Objective Function 才能工作的系统。
  2. WAM 不能自行改写用户的根本目标；外部证据可以提示"目标可能需要重新讨论"，但不能自动授权更换目标。
- **注意**：这条已确立，但它的**落地机制（Intent 如何表达）尚未确立**（见 B1 / OQ-01）。

### C-05 数值评分不是所有项目和研究的通用目标

- **内容**：分数、测试结果、性能、成本、截止日期是**具体场景的证据或约束**，不是跨任务通用的价值函数。
- **来源**：`docs/vision.md` §3.4
- **理由**：产品开发、开源建设、社科研究、论文复现均无充分代表成功的单一分数。

### C-06 WAM 需要理解 Situation 并形成 Judgment

- **内容**：必须区分 What matters? 与 What next?，先解决前者才能可靠解决后者。
- **来源**：`docs/vision.md` §4.3
- **性质**：Judgment 是核心研究对象，**不是** Planner 的同义词，**不是**优先级排序算法，**不是**一个名为 Wisdom Engine 的 Prompt 或评分器。

### C-07 行动必须受证据与真实结果约束

- **内容**：执行器声称"完成"不等于完成。证据应尽量来自真实世界。失败也必须形成信息。
- **来源**：`idea.md` Verifiability；`docs/architecture.md` §5 的五级证据阶梯
- **性质**：五级阶梯（执行 → 报告成功 → 可检查证据 → 满足验收 → 状态更新）**不得跳级**。

### C-08 验证行动是否成功 ≠ 判断行动是否值得

- **内容**：这是两个独立问题。一个成功的 Move 完全可能导致"停止当前方向"。
- **来源**：`docs/vision.md` §4.5；`docs/specifications/state-and-evidence.md` §4
- **性质**：混淆这两者是"能生成计划但不理解局面"的技术根因之一。

### C-09 执行器、技术栈、Agent 数量不应先于核心协作问题

- **内容**：先定职责与交互关系，再定代码模块。
- **来源**：`docs/foundation.md` §Boundaries（"Tech stack, number of agents, runtime architecture: implementation details, all deferred"）；`docs/vision.md` P7
- **性质**：**已被 10 次以上会话遵守**（仓库至今零代码，`docs/architecture.md` §7.1）。这是 WAM 最被验证的一条纪律。

### C-10 人暂时离开时 WAM 仍应能在授权范围内持续推进

- **内容**：Human Absent 时 WAM 仍应能恢复状态、自主判断、执行、检查、更新、重新判断；**没有可靠路径时暂停而非编造进展**。
- **来源**：`docs/architecture.md` §10
- **注意**：这是**要求**，不是**已具备的能力**（`docs/architecture.md` §10.2）。
- **边界**：不可逆、高风险、超出授权范围的行动必须停在人类决定节点。

### C-11 七条设计原则（防歧途）

- **内容**：P1 不要做成任务机器 / P2 不要把 Judgment 简化为 Priority Score / P3 不要把 Memory 简化为 Chat History / P4 不要让执行 Agent 成为状态唯一所有者 / P5 不要默认行动优于等待 / P6 不要把研究判断与执行验证混在一起 / P7 不要过早固定模块边界。
- **性质**：这七条是**对任何实现提案的否决依据**。提案违反其中任一条即不予采纳。

### C-12 治理机制：三层信任 + 晋升门

- **内容**：Evidence（`research/briefs/`）→ Proposals（`directions/`，**不可信**）→ Decisions（`docs/` + `workspace/`，权威）。未经验证不得进入官方结构。
- **来源**：`docs/foundation.md` §Development Governance；`directions/README.md`
- **性质**：本次新增的整套设计基线（`docs/vision.md` · `docs/architecture.md` · `docs/specifications/` · `docs/decisions/register.md` · `docs/specifications/acceptance.md`，即原 `docs/03`–`docs/08`）属于 Decisions 层。

### C-13 实验路径宣言：局部性结论

- **内容**：实验路径不是完整路径，只为一个局部性结论存在；结论到达即终止归档；失败是成功。
- **来源**：`experiments/README.md` §宣言（作者定义，2026-08-15）

---

### C-14 仓库知识结构：一类事实一个住处

- **内容**：`docs/` 按生命周期分层（`foundation` / `vision` / `architecture` + `specifications/` / `decisions/` / `development/`）；`research/` 承载知识层；`directions/` 保留但增加第三个出口 `parked`；`workspace/` 四文件是项目状态的唯一权威；`docs/README.md` 是唯一文档索引。**同一类事实只允许一个住处，第二处只能留指针。**
- **来源**：`REFACTORING_AUDIT.md`（13 条冲突、8 条结构问题）；`REPOSITORY_ARCHITECTURE.md`；`workspace/decisions.md` 2026-11-10
- **性质**：治理决定，**不改变任何技术设计**。`docs/development/mvp-plan.md` §5–§7 的原文搬迁（至 `docs/specifications/execution-contract.md`）逐行核对：694 个非空行，路径归一化后与迁移前逐行相同（4 处差异全为路径字符串），正文一句未改。
- **边界**：K-01（`workspace/*.md` 与 `.wam/state.json` 谁是权威）与 OQ-09/OQ-10 **未因本次重构被裁决**，仍按原状态挂着。

---

## 2. Current Design Baseline 当前设计基线

> 已收敛、适合继续设计的方向。**仍需与现有代码和实际开发约束对齐**——仓库当前零代码。

### B-01 核心循环

```
Intent + Situation → Judgment → Move → Execution → Evidence & Update → New Situation
```

- **状态**：基线。与 `docs/foundation.md` 六步协议的关系是**细化与修正，不是替换**（对应关系见 `docs/architecture.md` §2）。
- **关键修正**（相对六步协议）：
  1. Intent 需要被读，而不只是目标和进展。
  2. Judge 从"最高权重的一步"扩展为"什么**类型**的一步"（含等待/停止/请求人类）。
  3. Verify 明确区分"拿到证据"与"证据满足验收条件"。

### B-02 五个核心概念

Intent / Situation / Judgment / Move / Evidence & Update。

- **状态**：作为**职责划分**已确立。
- **明确不是五个软件模块**（`docs/architecture.md` §6）。把五个概念直接画成五个类的设计应被质疑。
- **现状差距**：Situation、Evidence 有载体；Move 部分成型；**Judgment 无过程载体，Intent 无持久载体**。

### B-03 Judgment under complexity 是关键研究对象

- **内容**：Judgment 是 WAM 最值得研究的部分。
- **六个启发式维度**（World/Situation、Knowledge、Values/Intent、Future/Counterfactual、Self/Metacognition、Time）是**观察视角**，不是模块清单，不要求逐项机械检查，不自动转成数值评分。
- **必须能产出的判断类型**（7 类）：执行 Move / 先调查 / 等待 / 缩小范围 / 改变路径 / 停止 / 请求人类判断。

### B-04 方向（Direction）暂不作为独立核心模块

- **内容**：方向信息可作为项目状态与 Judgment 输出的一部分。
- **理由**：不为追求对称而增加模块（P7）。
- **重新考虑的条件**：若 `docs/specifications/state-and-evidence.md` §1.1 的"当前方向 + 下一步为何值得"在实践中确实需要一个独立的承载者。

### B-05 持久项目记录：需要什么 vs 用什么实现

- **概念需求**（五项）：项目状态持久、来源可追溯、更新一致、能够恢复、防止状态无限膨胀。
- **实现判断**：现有的"append-only `log.md` + 当前状态快照（`state.md`/`goals.md`）+ git 版本"**已覆盖前三项**（持久、追溯、恢复）。
- **真正缺的是**：更新一致性（B5）、失败与否定证据的载体（B4）、状态膨胀控制（`docs/specifications/state-and-evidence.md` §7）。
- **结论**：**不引入** Event Log / State Ledger / Snapshot / Project Graph 作为独立机制。
- **Project Graph 明确推迟**：在判断质量未被验证前构建依赖图，风险是过早优化一个未被证明重要的维度（正是 P2 要防的事）。

### B-05b MVP 的持久化：单文件 JSON + git，不做事件溯源

- **取舍**（`docs/development/mvp-plan.md` §6.5）：`journal/` 保留**每次状态更新的记录**（不是完整事件溯源）；`state.json` 本身即全量快照；关系图不做。
- **理由**：完整事件日志的价值在需要重放时，而 MVP 不重放。**git 提供的是更强的可追溯性**（版本 + diff + 提交历史），且已经在那里。
- **一致性答案**：不是加锁或加事务，而是**循环中只有 I6 一个写入点**。
- **认识论防护的结构化落地**（`docs/development/mvp-plan.md` §6.3）：事实必须带 `source`（无 source 拒绝入库）；假设必须带 `validation_method`（否则降级为信念）；假设**不因时间流逝自动升级为事实**。这是 OQ-03 的最小防护，**不是完整解决方案**。

### B-06 执行层与 WAM 核心的边界

- **内容**：执行层可替换（换 Coding Agent、换模型、换工具），项目状态不随之丢失。WAM 持有状态，执行器借用状态。
- **来源**：`docs/architecture.md` §9；设计原则 P4

### B-07 认识论五分：事实/推导/假设/未知/不可观测

- **内容**：五类必须可区分。假设必须能说出验证路径，否则降级为信念。
- **现状**：语言层面有约定（`docs/foundation.md` 硬规则 4），**无结构保障**。
- **已知不可解**：无监督的 unknown-unknown 检测本质上是未解问题（`research/briefs/03-unknown-and-weight.md`）。
- **诚实的定位**：WAM 的贡献是**显式登记 + 人在回路**，不是自动检测。

### B-08 场景作为设计验证案例

- **内容**：Kaggle / 论文复现 / 开源建设 / 社会科学研究四类场景是**验收案例**，不是四套独立产品模式。
- **理由**：WAM 是否成立必须通过具体场景检验，不能只重复概念定义。
- **约束**：四类场景共用同一套核心循环与持久记录，差异只在 Intent 内容与 Evidence 形式。

### B-09 MVP 工程实现选择（2026-10-09 环境核查后定；**执行器一项已被 2026-10-28 修正，见 B-15**）

> **2026-10-28 修正**：本条中"codex-cli 作为首个 JudgmentProvider 与 MoveExecutor"**已被环境证伪**——codex 登录正常，但 `api.openai.com` 返回 403 地区限制（见 X-10）。执行器选择改由 **B-15** 承担；语言与持久化两项不变。

- **Python 3.13 + 零第三方依赖**：stdlib 已实测完整（json / subprocess / hashlib / uuid / datetime / pathlib / unittest / tomllib，17/17 存在）。原子写用 `tempfile` + `os.replace`。
- **codex-cli 0.138.0 作为第一个 `JudgmentProvider` 与 `MoveExecutor`**：已实测支持 `--output-schema`（schema 约束输出）、`--json`（事件流）、`-s read-only|workspace-write`（授权档位）、`exec resume`。
- **单文件 `.wam/state.json` 原子写** 作为循环权威状态；`workspace/*.md` 降级为只读证据来源。
- **DeepSeek Harness** 保留为未来执行器备选（npm 有 `@deepseek-ai/dsh@0.2.0-rc.2`，但本机未安装、未验证可运行）。
- **环境事实**：环境里的 `OPENAI_BASE_URL`（new.sharedchat.cc）**实测 403**，直连 LLM API 不可行。
- **实测记录与替代方案对比**：`docs/development/mvp-plan.md` §1.1–§1.2。三个选择都落在接口之后，**换实现不需要重写循环**。

### B-10 MVP 的接口集合：6 个，且刻意只有 6 个

- **保留**：I1 IntentProvider · I2 SituationBuilder · I3 JudgmentProvider · I4 MoveExecutor · I5 EvidenceVerifier · I6 StateRepository。
- **刻意不设**：DirectionProvider（方向是 Judgment 输出，见 B-04）· WeightCalculator / CandidateRanker / Scorer（直接违反 P2）· EventBus / Pipeline / Coordinator（循环是直线）· ReflectionService（自动摘要有无正确性保证未知，`docs/specifications/state-and-evidence.md` §7）。
- **抽取时机**：**T-14 在 T-09 竖切跑通之后**。在有真实实现之前抽接口等于按想象抽抽象。
- **逐项论证（边界问题 / 替换理由 / 输入输出 / 失败表达 / 未来实现）**：`docs/development/mvp-plan.md` §5.2

### B-11 三个必须先定的结构

- **I2 的 `situation` 三类字段**、**I3 的 `judgment` schema**、**I5 的 `acceptance` criterion 种类**必须先定——改它们等于改整个循环。其余可在 T-14 抽。
- **唯一不能推迟的**：Intent 与授权的表达。它们是判断的锚点，晚定等于循环重写（`docs/development/mvp-plan.md` §11.4）。

### B-12 三种状态必须严格区分

- **接口已定义** ≠ **接口已接入最小实现** ≠ **高级能力已实现**。禁止用"接口已定义"冒充"能力已具备"。
- **MVP 状态**：6 个接口全部为「已定义 + 已接入最小实现」；「高级能力已实现」**全部为否**。

### B-13 一处已记录的 M0 偏离：MVP 不在 WAM 仓库自身 dogfood

- **冲突**：`docs/foundation.md` 规定所有协作状态是 `workspace/` 四个 Markdown、人和 AI 直接读写。MVP 选择 `.wam/state.json` 作为机器权威。
- **处理**：`state.json` 是循环权威；`workspace/*.md` 只读为证据来源，不回写。
- **避开冲突的方式**：MVP 的核心验收对象是 `experiments/` 下的专用 fixture 项目，**不在 WAM 仓库上跑**。在 WAM 仓库上跑会立刻出现"人改 md / 机器改 json"的双权威问题。
- **性质**：这是对 M0 的一处**偏离**，不是推翻。M0 的四文件仍是人类协作的约定界面。记为 **OQ-18**。

### B-14 目标分类学：三维（层 × 承诺 × 证据），MVP 由格子推导（2026-10-28 定）

- **内容**：`docs/development/scope.md` 给出三维分类：**职责层 L0–L5**（信念/承诺/判断/行动/呈现/基底）、**承诺类型 G1–G5**（已承诺/探索/条件/推迟/拒绝）、**证据形式 E1–E4**（可执行/可观察/外部判定/论证）。
- **它解决的问题**：三个已发生的失效——(a) 把 E4（论证）写成 E1（已实现），实例是 `docs/development/mvp-plan.md` 896 行的计划里全部数据字段从未运行过；(b) 承诺类型混淆（`docs/development/mvp-plan.md` 的 A/B/C 里"留接口"既不是承诺也不是推迟）；(c) MVP 边界靠讨论而非推导。
- **MVP 推导规则**：`MVP-IN = {G1 且 E1/E2}` → 20 项；`MVP-MIN` 3 项（J6 停滞检测、U1 状态机、U6 scope 字段）；`MVP-OUT` 12 项（合计 35 格）。**清单不得直接改，只能改格子或改规则。**
- **最重要的产出**：§3.2 的类型声明——**MVP 只主张 T1（收敛型）+ T2 的 L1–L2，T3/T4 是 Phase 4 的检验对象，不是 MVP 的承诺**。没有这一句，四类场景的文档会被读成"MVP 支持四类"。
- **新增两格**：G3（条件承诺）与 G5（拒绝）在原有四态（`docs/decisions/register.md` §0）中没有对应。G5 把"不引入 Event Log / 不建 Project Graph / 不设 WeightCalculator"等散落判断变成可引用的拒绝清单。

### B-15 执行器选择被环境证伪：codex 不可用，改 DSH headless 为主、人作兜底（2026-10-28）

- **实测**：`codex-cli 0.138.0` 存在且**已登录**；`codex exec --ephemeral -s read-only` 请求 `api.openai.com/v1/responses` 返回 **403 `Country, region, or territory not supported`**（cf-ray HKG，重连 7 次后失败）。认证不是问题，**地区限制是**。
- **结论**：**B-09 的 codex 选择作废。** 新顺序（`docs/development/roadmap.md` §4 D1）：
  1. **首选** `dsh --profile headless "<task>"`——帮助文本实测存在（"answer one task, print the result, and exit"），走已验证可用的 DeepSeek provider；**但该 profile 未安装**（`~/.dsh/profiles` 只有 `desktop`/`web`），需作者执行一次初始化。
  2. **兜底** 人作 `MoveExecutor`（LLM 只做判断）——零依赖，且本身就是 `docs/development/mvp-plan.md` §5.2 认可的 I4 实现（"人工执行 + 手工填证据"）。
  3. **不作首选** DeepSeek API 直连（`DEEPSEEK_API_KEY` 在 DSH 凭据库中有引用，但结构化输出能力未验证）。
- **不受影响的**：I1–I6 六个接口与整个循环。**这正是 B-10 主张"接口先于实现"的兑现时刻**——换执行器不需要重写循环。
- **性质**：已确立的环境事实 + 基线级选择。若 headless 路线在原定 30 分钟内调不通，直接走兜底，**不视为失败**。

### B-16 交互表征：注意力状态机（10 状态 / 6 模式），与 Move 生命周期正交（2026-10-28 定）

- **内容**：`docs/architecture.md` §12 定义 **Agent State**（注意力状态，10 个：SITUATING / DECIDING / DISPATCHING / ACTING / VERIFYING / INVESTIGATING / EXPLORING / WAITING / ASKING / STOPPED）与 **Move 生命周期**（物的状态，`docs/specifications/state-and-evidence.md` §3.2 权威）是**两个正交轴**，不是同一状态机的两种画法。
- **推导判据**：**用户行为区分测试**——两个状态合并 iff 用户在该状态下该做的事相同。按此判据：`WAITING` 与 `ASKING` **不可合并**（前者用户无事可做，后者用户是唯一能解锁的人），这是整张表里唯一不可妥协的一处。
- **机器 10 / 呈现 6** 的理由：机器要无歧义，人要低焦虑；`SITUATING` + `DECIDING` 对用户是同一件事，故在呈现层合并。
- **六条不变量**（E1 可测）：在等谁必填；只有 WAITING/ASKING 允许无证据停留超时；进 ACTING 前 acceptance 已持久化；DISPATCHING 是唯一允许提升 sandbox 档位的状态；状态与 Move 状态一致；每次迁移写 journal。
- **形式基础**：statechart（层次 + 正交区域）而非平面 FSM——两个正交轴若塞进一个平面机，状态数是乘积（10 × 7 = 70）。**这是分两轴的独立依据**，不只是"两个受众不同"。
- **MVP 最小实现**：迁移记录 + CLI 头部四问 + `assert_state_invariants()`。**不做** GUI（U4 推迟）。


---

## 3. Working Hypothesis 待验证假设

> 有吸引力，但**尚未证明必要或正确**。不可直接实现。

### H-01 Event Log / State Ledger / Snapshot / Project Graph 四机制

- **假设**：项目状态应由这四种机制共同承载。
- **当前判断**：❌ **不需要**。见 B-05——现有组合已覆盖核心需求。
- **验证条件**：只有在现有组合实际暴露痛点时才重开。

### H-02 单一 Active Move 作为推进治理边界

- **假设**：同时只有一个 Active Move 可作为治理单位。
- **当前判断**：⚠️ **倾向采用，但边界必须明确**。
- **边界（防过度约束）**：不意味着一次只能调一个工具、不意味着只能有一个 Agent、不意味着一切操作机械串行。并行由该 Move 的边界、依赖和风险决定。
- **验证条件**：阶段二 2c 之后。若实际多个并行 Move 反复产生状态冲突，说明边界定义有误。

### H-03 Judgment 需显式候选方案比较与反事实推演

- **假设**：Judgment 应显式比较多个候选方案并做反事实推演。
- **当前判断**：⚠️ **未验证**。Future/Counterfactual 维度确实包含"不行动"这个选项，但"显式候选比较"是否必要、是否成本可接受，未知。
- **风险**：显式候选比较容易退化成"看起来很认真的长文本"，且可能诱发分数化（P2）。
- **验证条件**：阶段二 2d 的判断质量检查中，观察判断输出是否真的因比较而改变。若没有，该假设可弃。

### H-04 权重档位与关键路径计算作为 Judgment 输入

- **假设**：`goals.md` 的三档权重（critical path / enhancement / noise）与目标 DAG 的关键路径计算，可作为 Judgment 的输入信号。
- **当前判断**：⚠️ **作为输入信号采纳，但不等于 Judgment**。
- **必须遵守的约束**：人类标注的 tier 不能被计算结果自动覆盖；计算结果也不能自动改写人类 tier。
- **理由**：依赖结构 ≠ 重要性。一条不阻塞任何事但直接验证核心假设的实验，可能比长依赖链上的任务更重要；反之在关键路径上但已被证伪的路径，计算上仍在关键路径上，却已不值得走。
- **验证条件**：`directions/weight-first/` 的 promotion gate（两周内计算出的关键路径是否真的改变或阻止过一次优先级决策）。

### H-05 特定数据图结构表达项目依赖

- **假设**：项目依赖应该用图结构（DAG 等）表达。
- **当前判断**：⏸️ **推迟**。见 B-05。
- **验证条件**：阶段二暴露真实的依赖查询痛点，且平面 `goals.md` 确实无法表达。

### H-06 让 WAM 在特定规则下自动更新某些意图或方向字段

- **假设**：某些意图/方向字段可在规则下自动更新。
- **当前判断**：❌ **直接违反 C-04**。WAM 不能自行改写用户的根本目标。
- **唯一例外**：**不涉及根本目标**的实现性字段（如"下一步的时间盒已过期"）。
- **边界**：这条边界必须由作者裁决，不由实现者自行解释。

### H-07 Direction 独立为持久状态实体

- **假设**：方向值得拥有独立持久载体（而非 Judgment 输出的派生结果）。
- **当前判断**：⚠️ 未验证。见 B-04。
- **验证条件**：`workspace/` 恢复实验（`docs/specifications/state-and-evidence.md` §6.2 第 10 项"下一步为什么值得"）中，若方向信息无法从记录中有效恢复，则重开。

### H-08 自动摘要 / 状态压缩 / 遗忘

- **假设**：可用自动摘要控制状态膨胀。
- **当前判断**：❌ **MVP 不做**。`research/briefs/02-memory-and-state.md`：LLM 生成的反思与摘要有无正确性保证。在没有正确性保证前自动压缩权威状态，是把不确定性引入信任根。
- **验证条件**：需要先有"摘要正确性"的评价方法（目前不存在）。

### H-09 共享上下文作为独立组件（多层级 + 显式探索边界），位于"信息源"职责空间

- **假设**：WAM 的协作基座是分层、带显式边界的共享上下文，而非 agent 间消息（作者 2026-10-27）。
- **当前判断**：⚠️ **未验证。** 三个子假设里，H-a（消息不是有效协调方式）有外部支持但**非受控实验**；H-b（独立组件能降低状态失同步）是本方向的核心且完全未验；H-c（默认单 Agent 不弱于多 Agent 编排）与 Anthropic 的广搜报告存在张力。
- **处置**：进 `directions/shared-context/`（提案层）。**MVP 只带 `scope` 字段，不带服务**（`docs/development/scope.md` U6）——单 agent 时没有第二个读者/写者，scope 机制无从验证。
- **最可能发生的失败**：**F-1，scope 字段加了但从未被任何代码读取过。** 一个没人读的字段等于没有，只多了一层"我们考虑过并发"的自我安慰。
- **验证条件**：`directions/shared-context/` §6 的三阶段实验；阶段 2（写集相交必须**阻塞并报告**，不得静默覆盖）是唯一硬判据。

### H-10 默认单 Agent（Miracle Agent）+ 并发调用多工具实体，拒绝 agent 间对话式调度

- **假设**：默认只启用一个全局 Agent，它可同时调用多个工具注册实体；多 Agent 只在共享上下文 scope 机制被证明有效后才允许接入（作者 2026-10-27）。
- **当前判断**：⚠️ **倾向采纳，且已升级了拒绝的依据**。`docs/development/scope.md` M6 从"P7 的推迟"升级为 **G5 拒绝**——依据是 `research/external-assets.md` A1（Cognition 的两条上下文原则，全文已读）与 A2（MAST：14 种失败模式聚为 3 类，摘要已读）。
- **必须守住的措辞**：拒绝的是**"agent 间对话式调度"**，不是"并发"。`docs/development/scope.md` M5（一个 Move 内并发调多工具）是 **G1 已承诺**，与 M6 不矛盾。
- **唯一的窄例外**：子任务同时满足 ① 彼此独立 ② 只读 ③ 结果可被主 Agent 独立复核。三条件缺一不许并发。
- **验证条件**：`directions/shared-context/` §2 的 F-2（在真正可并行的任务上，单 Agent 顺序执行的耗时/质量不差于并发）。若 F-2 成立，H-10 的措辞需要放宽。

---

## 4. Open Question 开放问题

> 仍影响设计或正式开发。**每一条都标注了它阻塞什么。**

| # | 问题 | 阻塞什么 | 谁能回答 |
|---|---|---|---|
| **OQ-01** | **Intent 的最小数据表达是什么？** | 阶段 2a 全部；能力 #1、#9；Human Absent Mode 前置 | 作者 + 设计 |
| **OQ-02** | **如何表示含糊、复合或相互冲突的意图？** 目标可能互相矛盾时怎么办？ | 场景 C（开源建设）、场景 D（社科） | 作者 + 实验 |
| **OQ-03** | **如何避免将假设误当成事实？** | `docs/specifications/state-and-evidence.md` §2 的四条缓解手段是否有效 | 实验（阶段二 2c） |
| **OQ-04** | **Situation 的最小必要状态是什么？** 哪些必须持久、哪些可派生？ | 阶段一查询设计、状态膨胀控制 | 实验 |
| **OQ-05** | **哪些状态变化需要证据、哪些需要人工授权？谁在什么时候写哪几个文件？** | 一致性（B5）；多会话并发写 `log.md`（`workspace/state.md` 已列此 unknown-unknown） | 设计 + 作者 |
| **OQ-06** | **如何避免项目状态无限膨胀？** | 长期可维护性 | 实验（阶段二期间观察） |
| **OQ-07** | **Judgment 如何把握行动、调查、等待、停止之间的选择？** | 能力 #4；这是 WAM 最难的问题 | 实验（阶段二 2d） |
| **OQ-08** | **Move 的边界应该如何确定？** 什么样的行动算一个 Move？ | 能力 #5；H-02 的边界定义 | 设计 + 实验 |
| **OQ-09** | **WAM 与 Sponge 是什么关系？** | 是否需要写 WAM → Sponge 的映射；是否需要检查 Sponge 侧描述的 WAM 承诺是否与本仓库当前设计一致 | **作者裁决** |
| **OQ-10** | **是否需要绑定某个执行平台？** DSH 已验证，Hermes 无法核实，Sponge 侧另有口径 | 阶段二的执行环境 | 作者裁决 |
| **OQ-11** | **WAM 是否仍应建立在四文件 Markdown + git 上？** 还是需要结构化存储？ | 阶段一的全部解析逻辑 | 作者 + 实验 |
| **OQ-12** | **如何判断某个未知是否值得调查？** | 避免陷入"把所有未知都变成待办" | 实验 |
| **OQ-13** | **如何保留历史教训，又不让过往路径支配未来决策？** | 失败信息回写的平衡 | 实验 |
| **OQ-14** | **哪些能力必须进 MVP，哪些可以推迟？** | ✅ 已给出阶段性答案（`docs/development/mvp-plan.md` §4），但需作者确认 | 作者确认 |
| **OQ-15** | **三档权重是否需要更细粒度？如何低成本维护？** | `workspace/state.md` 已列此 unknown；与 H-04 相关 | 实验 |
| **OQ-16** | **"反向机"（作者草图）的语义是什么？** | global-route 的第二个切片；`workspace/state.md` 已标为"pending author confirmation" | 作者 |
| **OQ-17** | **何时真实使用会迫使四文件格式演化（state-v2 触发条件）？** | state-v2 的开启时机 | 实验 |
| **OQ-18** | **WAM 仓库自身的 dogfood 如何处理双权威？** `docs/foundation.md` 规定状态是 `workspace/*.md`；MVP 用 `.wam/state.json`。在 WAM 仓库上跑就有两个写入方 | MVP **不阻塞**（验收对象是专用 fixture 项目）；阻塞"用 WAM 跑 WAM 自己" | 作者裁决（B-13） |
| **OQ-19** | **codex 认证在目标环境是否可用？** 本轮沙箱禁止访问 `~/.codex`，只实测到版本 0.138.0 存在 | 不阻塞 T-01–T-05；**阻塞 T-06/T-08** | 一次 `codex exec --ephemeral -s read-only` |
| **OQ-20** | **sandbox 档位的推导规则如何定？** codex 提供三档，但"从 `authorization` 映射到档位"的规则是本项目设计，未验证 | 不阻塞开工（Phase 1 用最保守版本：默认 `read-only`，需批准才升级）；阻塞"自动执行"的可信度 | Phase 2 |
| **OQ-21** | **Judgment 的 schema 稳不稳定？** | 若调 3 次仍不稳定，说明 I3 边界定错 | Phase 1 期间观察 |
| **OQ-22** | **开源自建项目（场景 C）的验收对象是什么？** 无单一指标，"做完了"需外部判定 | 不阻塞 MVP（Phase 4 才需要）；阻塞 Phase 4 的案例设计 | 作者 + Phase 3 之后 |
| **OQ-23** | **运维型任务（T5，"保持不坏"）如何表达 Intent？** 什么都不做是否算成功？ | 不阻塞 MVP；阻塞"长期项目"这一主张的完整性（长周期项目里此类任务占比很高） | 作者 + 实验 |
| **OQ-24** | **scope 写集相交时应当阻塞还是串行化？** 阻塞会暴露设计错误，串行化会隐藏它但更顺滑 | 不阻塞 MVP（只带字段）；阻塞 `directions/shared-context/` 的实验结论 | 实验 |
| **OQ-25** | **10 个状态是否过多？** 社区产品在收敛到 3 个可见状态，而 WAM 主张 10 个 | 不阻塞 MVP（U1 为 MVP-MIN）；阻塞"交互表征数量"的最终答案 | W4 之后的实际使用：作者是否真的看第 6–10 个状态 |
| **OQ-26** | **`dsh --profile headless` 的输出能否被可靠地约束为 JSON？** profile 未安装，能力只见于帮助文本 | **阻塞 `docs/development/roadmap.md` W3 的 JudgmentProvider** | W0 的一次命令（`docs/development/roadmap.md` §4 D1） |
| **OQ-27** | **J6 的停滞判据（连续 3 个 Move 无新事实 → 转向）是否有效？** 已有文献讨论"agent 循环把停滞误当进展 + 自我评估偏差"，本会话未读全文 | 不阻塞 W6 之前的任何工作；**若 W2 前未读该文献，则 W6 不实现 J6** | 读 `arXiv:2607.25152`（`research/external-assets.md` §2 E1） |


---

## 5. 已识别的文档与现实不一致

> 这一节记录**核查中发现的事实冲突**，用于防止文档继续传播错误信息。

| # | 不一致 | 核查结果 | 处理 |
|---|---|---|---|
| **X-01** | `directions/global-route/README.md`、`directions/agent-plugin/README.md` 称 **Hermes Agent** 为 "the platform this project is developed on" | `D:/github projects/` 下**不存在** Hermes 目录；`.hermes` 仅存在于 `statuz/` 与 `Oasis AdaMem/`，与 WAM 无关 | 已标注为过期表述（`docs/architecture.md` §7.3）。**未直接改写原文件**——方向 README 属 proposals 层，且改写需作者确认。记为 OQ-10 |
| **X-02** | Sponge 侧（`D:/github projects/Sponge/研发/03_架构与生态位.md`）把 WAM 定位为「基于 Sponge 构建的应用层衍生物」，并写入其收敛验收标准 | WAM 仓库 29 个 tracked 文件中 "Sponge" 出现 **0 次**；本仓库所有权威文档均表述"技术栈未定" | 记为 OQ-09，**不单方面裁决**。在裁决前 WAM 仓库维持"技术栈未定" |
| **X-03** | Sponge 侧描述的 WAM 承诺为「四重缺失 + 状态失同步；状态模型四文件 + 六步循环 Read→Wait→Judge→Do→Verify→Write」 | 其中**六步循环已过时**：本仓库 `docs/architecture.md` §2 已对它做了三处修正（Intent 需被读；Judge 扩展为类型选择；Verify 分两级） | 若采纳 Sponge 定位，需同步更新 Sponge 侧描述。记为 OQ-09 |
| **X-04** | `workspace/log.md` 最近条目日期为 2026-08-15，最后一次 commit 为 2026-08-13，当前为 2026-10-09 | **约 8 周无活动记录**；`workspace/` 存在未提交改动 | 本次任务已按六步协议更新 `workspace/`。**注意：`workspace/` 的改动仍未提交**，需作者自行决定提交时机 |
| **X-05** | `docs/development/dashboard-plan.md` 规划 `scripts/dashboard.py`（Python） | DSH 侧已验证平台为 TypeScript（`@deepseek-ai/dsh-*` npm 包） | **已解决**：`docs/development/mvp-plan.md` §1.2 选了 Python，理由是 stdlib 已实测完整且零安装风险；Dashboard P4 与 WAM CLI 共用解析逻辑，语言一致不再有冲突 |
| **X-06** | `directions/global-route/README.md` 引用 "Hermes skill" 作为 stage 2 的载体 | 本机 `codex-cli 0.138.0` 已安装且支持 `codex exec --output-schema/--json/-s`，是一个**已实测可用**的执行器候选 | 记为 B-09；Hermes 的核实失败仍记为 X-01 |
| **X-07** | 环境变量 `OPENAI_BASE_URL` + `OPENAI_API_KEY` 存在，看起来"有 LLM 可用" | 实测 `/models` 与 `/chat/completions` 均 **HTTP 403**（网关回"该接口未接入公益站独立网关"）。**代码里不能假设这个端点可用** | 记为 B-09；这也是"MVP 不直连 LLM API"的原因 |
| **X-08** | DeepSeek Harness 被 `experiments/README.md` 记录为已验证的执行环境 | npm 上有 `@deepseek-ai/dsh@0.2.0-rc.2`，但本机 `node_modules` **未安装**，本轮未验证可运行 | 记为 B-09 的备选；不阻塞 MVP（I4 是接口） |
| **X-09** | `docs/development/mvp-plan.md` §1.1 记 Python 为 **3.13.12** | 2026-10-28 实测本机为 **3.14.2** | 无实际影响（零第三方依赖）。记录以免后续按 3.13 的特性写代码 |
| **X-10** | `docs/development/mvp-plan.md` §1.2 / B-09 把 **codex-cli 作为首个 JudgmentProvider 与 MoveExecutor**，并称"全部所需 flag 已实测" | flag 确实存在，**但执行被地区限制**：`api.openai.com` 返回 403 `Country, region, or territory not supported`（cf-ray HKG）。codex **已登录**，问题不在认证 | **已修正为 B-15**：改 DSH headless 为主、人作兜底。这是本仓库第一次出现"实测通过但结论仍被推翻"的情形——**验证了一个属性，不等于验证了它能不能用** |
| **X-11** | 全部 `docs/` 的版本戳为 **2026-10-09**，`docs/decisions/register.md` 写于该日 | 本会话实际日期 **2026-10-28**，间隔 19 天；同一天（10-28）发现 codex 403、Python 3.14.2，并新增 `docs/development/scope.md`、`docs/development/roadmap.md`、`research/external-assets.md` | 这三份以 2026-10-28 为版本戳；`docs/development/mvp-plan.md` 保留 10-09 版本戳并加修正指针（**不静默改写历史版本**） |
| **X-12** | `site/details.html` §LIVE STATUS 自称 "Snapshot of workspace/ ... this section mirrors it"（"本区块如实镜像"） | 实为 **2026-08-07 冻结快照**：仍写"4 个方向"，无 `docs/03`–`11` 任何内容，无 codex 被证伪一事。与 README / `workspace/state.md` 三处不一致 | 2026-11-10 改标为 frozen snapshot（不再声称镜像）；内容与设计不动 |
| **X-13** | 格子数：`README`、`workspace/state.md`、`workspace/goals.md` 写 **35**；`docs/development/scope.md` §1 写 **36**，§4.2 四集合为 20+3+1+12 | **36 才对**：摘要漏掉了 `MVP-SEAM`（1 项）这一类 | 2026-11-10 已统一为 36 并补上 SEAM；`scope` §4.2 为权威 |


---

## 6. 使用规则

1. **引用本文档时必须带状态标记。** 说"这是已确立的"和说"这是个假设"是两种完全不同的话。
2. **发现 Working Hypothesis 被当成 Confirmed 使用** → 这是本文档存在的意义所在，应立即纠正。
3. **新增决策** → `workspace/decisions.md` 记事件，本文对应位置记状态。
4. **Open Question 被回答** → 从本表移出，写入日志，并归入对应状态。
5. **本表不记录实现细节**（类名、字段名），那些在代码里。
