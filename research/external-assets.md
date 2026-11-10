# External Assets — 外部可借鉴的工作与取舍

> 版本：2026-10-28 · 状态：**Evidence 层草案**（每条已标注核实程度；未读全文的一律标 B/C，不得当成结论引用）
> 方法：沿用 `reference/WORKFLOW.md` 的评估纪律——证伪比采纳重要，代价必须写出来。
> 本文档只回答一个问题：**外部世界有哪些东西可能帮到 WAM，以及我们为什么只拿其中一部分。**

---

## 0. 核实程度分级（先读这一节）

| 级 | 含义 | 允许的用法 |
|---|---|---|
| **A** | 本会话读到了**原文/全文** | 可以作为论据引用 |
| **B** | 读到了**摘要或标题 + 权威页面**，未读全文 | 只能作为"存在这个说法"的证据，不得转述其结论 |
| **C** | 只有二手转述（搜索结果、他人总结） | **不得引用**，只能作为"去读原文"的线索 |

**本仓库已因一次编造文献被标记过**（`research/briefs/03` caveat：Ramírez & Burrage 在 Crossref/arXiv/Semantic Scholar 均未找到，已标记未编造）。本节遵守同一条纪律：**没读到的东西不写成结论。**

---

## 1. 五条结论（先给判断，再给材料）

| # | 结论 | 对 WAM 的直接影响 |
|---|---|---|
| **1** | **作者"不用传统 Multi-Agent"的判断，有独立的外部支持，而且支持它的是工业界而非学术界** | M6 从"我们的偏好"升级为"有依据的拒绝"（`docs/development/scope.md` G5） |
| **2** | **"共享上下文作为组件"这个定位，恰好是别人明确说"没人认真在做"的空位** | `directions/shared-context/` 的差异化不是想象出来的 |
| **3** | **黑板架构（blackboard）是最接近的先例，但它的第三个部件必须被拒绝** | 借鉴知识源 + 共享数据结构；拒绝 control（仲裁器） |
| **4** | **状态表征的形式基础是 statechart 而不是 FSM** | 解释了为什么是"10 状态 / 6 模式 / 两个正交轴"而不是"一个 10 状态机" |
| **5** | **最该先读的一篇文献，恰好直接讨论 P1（活动 ≠ 进展），但本会话没读到全文** | J6（停滞检测）有一篇必读前置，否则我们是在重复别人的工作而不自知 |

---

## 2. 材料（按 WAM 的问题分组）

### A. 反多 Agent —— 支持 M6 的既有判断

| # | 来源 | 它说什么（核实程度） | 对哪一格有用 | 裁决 |
|---|---|---|---|---|
| A1 | [Don't Build Multi-Agents](https://cognition.com/blog/dont-build-multi-agents) — Cognition (Walden Yan), 2025-06-12 | **A（全文已读）** 两条原则：① *Share context, and share full agent traces, not just individual messages*；② *Actions carry implicit decisions, and conflicting decisions carry bad results*。作者主张**默认排除**违反这两条的任何架构；并指出"没人认真在做跨 agent 上下文传递这件事" | M6、U3、`directions/shared-context/` | **adopt（作为架构不变量）** |
| A2 | [Why Do Multi-Agent LLM Systems Fail?](https://arxiv.org/abs/2503.13657) — MAST, arXiv:2503.13657 | **B（摘要已读）** 1600+ 条 trace、7 个框架；14 种失败模式聚为 3 类：**系统设计问题 / agent 间失配 / 任务验证**；人类标注一致性 κ=0.88。摘要自述这些失败"需要更复杂的解法" | `directions/shared-context/` 的设计检查表；K5、M2 | **adapt（当检查表用，不当解法用）** |
| A3 | [Anthropic: How we built our multi-agent research system](https://simonwillison.net/2025/Jun/14/multi-agent-research-system/) | **B/C（二手总结，未读官方原文）** 多 agent 在**广度优先的检索任务**上有收益，代价是显著更高的 token 消耗 | M6 的唯一允许破例 | **defer（作为"窄例外"记录，不作架构）** |

**为什么只拿一部分**：A1 的两条原则是**不可违背的**，而 A2 显示违反它们的代价是系统性的、不是偶发的。A3 是唯一的反例，但它的任务形状（可分解为 N 个独立只读子问题）恰好是 WAM 的**长线聚合任务**的反面——这一点必须写清楚，否则"Anthropic 也用多 agent"会变成无休止的重新论证。

> **窄例外的准确表述（写进 `directions/shared-context/`）**：
> 只有在「子任务彼此独立 **且** 只读 **且** 结果可被主 agent 独立复核」时，并发才被允许。三个条件缺一不许并发。WAM 的 Move 执行大多是写操作，因此默认不满足。

---

### B. 共享上下文 / 黑板 —— 最接近的先例

| # | 来源 | 它说什么（核实程度） | 对哪一格有用 | 裁决 |
|---|---|---|---|---|
| B1 | [SE-Blackboard: A Shared-State Architecture for Multi-Agent Software Engineering Pipelines](https://ieeexplore.ieee.org/document/11527206) | **B（标题 + 权威页面存在，未读）** 标题即主张：**共享状态**架构 | U6、`directions/shared-context/` | **defer（第一篇待读）** |
| B2 | [LLM-Based Multi-Agent Blackboard System for Information Discovery in Data Science](https://neurips.cc/virtual/2026/loc/atlanta/poster/151426) | **B（标题存在，未读）** 把黑板用在 LLM 多 agent 的数据发现上 | 同上 | **defer（第二篇待读）** |
| B3 | 经典黑板架构：Hearsay-II、BB1；综述见 Nii, *Blackboard Systems*, AI Magazine 1986 | **C（本次未复核，属常识层）** 黑板 = 三个部件：**知识源 knowledge sources（无状态专家）**、**黑板数据结构（共享状态）**、**控制 control（仲裁下一个该谁动）** | U6 的形式骨架 | **adapt（三分之二）** |

**这是本文档最精确的一条取舍**：

| 黑板三部件 | WAM 的处置 | 理由 |
|---|---|---|
| 知识源 knowledge sources | **采纳**：就是"工具注册实体"/"被调用的能力"，无状态、可并发 | 与作者"Miracle Agent 可并发调用多个工具注册实体"完全同构 |
| 黑板数据结构 blackboard | **采纳**：就是"共享上下文"，多层级 + 显式探索边界 | 这正是作者说的"位于信息源职责映射空间内的独立组件" |
| 控制 control（仲裁器） | **拒绝** | 仲裁器就是调度器——`docs/development/scope.md` M6 拒绝的正是它。WAM 用**单一全局 Agent 的判断**替代仲裁 |

> 一句话：**WAM 要黑板的"板"，不要黑板的"主席"。** 这句话可以直接拿去做 `directions/shared-context/` 的题眼。

**为什么这一组仍然只到 defer**：B1/B2 都未读。在读到之前，我们不能声称"共享上下文作为组件是原创的"——**只能声称"我们知道最接近的先例是什么，且我们知道要拒绝它的哪一部分"**。这是诚实的差异，也是可验证的差异。

---

### C. 状态与恢复

| # | 来源 | 它说什么（核实程度） | 对哪一格有用 | 裁决 |
|---|---|---|---|---|
| C1 | [LangGraph Interrupts](https://docs.langchain.com/oss/python/langgraph/interrupts) | **B（官方文档页存在）** 中断是一等原语：停在某点、等人、用检查点恢复 | U1、S1、M4 | **adapt（概念）** |
| C2 | [Temporal: durable execution for LangGraph](https://temporal.io/blog/temporal-langgraph-plugin-durable-execution) | **B（官方博客存在）** 用确定性重放实现"进程死了工作还在" | S1、M4 | **reject（作为依赖）/ adopt（作为测试思路）** |

**为什么拒绝 Temporal 类 durable execution 引擎**：项目当前的全部持久化需求是"一个 JSON 文件、单写点、原子替换、幂等键"（`docs/development/mvp-plan.md` §6.5、§7.3）。引入重放引擎会把 1% 原则换成一个运维负担，而它解决的问题（崩溃后状态一致）已经被"单写点 + `os.replace`"覆盖到 MVP 所需的程度。

**但要采纳它的一个想法**：*determinism*. Temporal 的恢复之所以可靠，是因为重放是确定性的。WAM 的等价检验是——

> **kill 之后重启，`journal` 的后续序列应当与"没 kill 过"的世界一致，除非新证据进入。**

这条可以变成 W5 的一个测试思路，而**不需要引入引擎**。这是"借鉴机制"与"引入依赖"的分界线。

**C1 采纳的只是概念**：中断要能被持久化，而不是一个异常。这与 `docs/architecture.md` §12 的 `WAITING` / `ASKING` / `STOPPED` 三态是一致的——**它们不是错误处理，是正常状态**。

---

### D. 交互表征 —— 回答"要加多少状态"

| # | 来源 | 它说什么（核实程度） | 对哪一格有用 | 裁决 |
|---|---|---|---|---|
| D1 | Harel, *Statecharts: A Visual Formalism for Complex Systems* (1987) | **C（经典，本次未复核原文）** 两个机制解决状态爆炸：**层次（composite state）** 与 **正交区域（orthogonal regions）** | U1、U5 | **adopt（形式基础）** |
| D2 | [Microsoft HAX 人机交互指南](https://github.com/miguelferre/human-ai-governance)（HAX-18 审计工具）与 Google PAIR | **B（工具与指南存在）** 18 条指南里与本项目直接相关的三条：*make system status visible*、*convey consequences*、*support efficient correction* | U2 的验收清单 | **adapt** |
| D3 | 社区实践：[visible session states — Working + WaitingAgent + Done](https://github.com/xmiksay/entanglement/commit/563ba57789f36e436852efdd8f42db410dad0dd9) | **B（一个提交记录）** 有产品在收敛到 **3 个**可见状态 | 对 U1 的**反向信号** | **记录，不采纳** |

**D1 是本节最有用的发现**：我们不需要"一个 10 状态机"，我们需要**一个 statechart**——因为 WAM 天然有两个正交区域（注意力的状态 × 物的状态），而把正交的东西塞进一个平面状态机会导致状态数乘积爆炸（10 × 7 = 70）。**这正是 `docs/architecture.md` §12.1 决定分两个轴的独立依据**，不只是"两个受众不同"。

**D3 必须被记录，因为它是反对意见**：如果真实产品收敛到 3 个状态，我们凭什么要 10 个？答案是——**那 3 个状态是给"一次对话内"的 agent 用的；WAM 的状态要服务"跨会话、跨天、跨中断"的重新同步，而在这个时间尺度上，`WAITING` 与 `ASKING` 的区分是决定性的**（前者你别回来，后者只有你能解锁）。
**但这条答案是可错的**：若 W4 之后作者发现自己从不看第 6–10 个状态，那就砍到 3 个模式 + 1 个"在等谁"。**记入 §5 的自我怀疑。**

---

### E. 判断质量与停滞 —— 最该先读的一组

| # | 来源 | 它说什么（核实程度） | 对哪一格有用 | 裁决 |
|---|---|---|---|---|
| E1 | [When Do Agent Loops Mistake Stagnation for Progress? Self-Evaluation Bias and Externally Grounded Verification in Long-Running Autonomous LLM Agent Loops](https://arxiv.org/abs/2607.25152) | **B（标题 + 检索摘要；本会话取全文被 429 限流，未读）** 标题同时命中 P1（活动量≠进展）与 C-07（外部接地验证） | **J6、J3、C-08** | **defer → 列为 J6 的必读前置** |
| E2 | [METR: Measuring AI Ability to Complete Long Tasks](https://arxiv.org/abs/2503.14499) | **B（arXiv 页面存在；具体数值以原文为准）** 以"50% 成功率下的任务时长"作为能力度量，该时长约每 7 个月翻倍 | **Move 的尺寸**（M1）、W8 失败分析 | **adapt（用法如下）** |

**E1 为什么最重要**：`docs/development/scope.md` J6 提出的停滞判据（连续 3 个 Move 无新事实 → 转向）是**我们自己想的**，而这篇标题暗示别人已经在研究同一件事，且结论可能更细（"自我评估偏差"意味着**系统自己判断"我在进展"是不可信的**——这直接威胁我们让 LLM 自己产出 `why` 的设计）。**在 W6 实现 J6 之前必须读它**，否则我们可能在实现一个已知无效的方案。

**E2 的实用价值不是"AI 能做多长时间的任务"，而是反过来用**：

> **一个 Move 的复杂度，必须显著低于模型的时间视野。**

如果模型在 50% 成功率下的时间视野是若干小时，那么一个"预计要 3 天"的 Move 的失败不是执行问题，是**边界切错了**。这把 `docs/development/scope.md` OQ-08（Move 的边界怎么定）从纯设计问题变成可用外部数据约束的问题。**这是本次调研里唯一一条能直接改工程决策的外部输入。**

**为什么 E2 只到 adapt**：METR 测的是"任务时长"与"成功率"，不是"判断质量"。它约束的是**尺寸**，不是**智慧**。把两者混起来正是 P6（不要把研究判断与执行验证混在一起）要防的。

---

### F. 上下文工程（与既有判断一致，只作旁证）

| # | 来源 | 它说什么（核实程度） | 裁决 |
|---|---|---|---|
| F1 | Anthropic *Effective context engineering for AI agents*；Chroma *context rot* 技术报告 | **C（二手）** 长上下文中信息利用率下降，需要"策展"而非"堆叠" | **defer**：与 `docs/specifications/state-and-evidence.md` §7 的立场一致（先测量长度，再决定压缩），不构成新决策 |
| F2 | ADAMEM verbosity pathology（已在 `reference/enhancement/adamem.md`） | **已入库** 检索轨迹越多，性能反而下降（52.1% → 47.8%） | 已被采纳为设计准则（`wam goal next` 只输出一行） |

---

## 3. 反借鉴清单增量（进 `reference/WORKFLOW.md` 的表）

| 机制 | 为什么拒绝 |
|---|---|
| **黑板架构的 control 组件（仲裁器）** | 它就是调度器，就是 M6 拒绝的东西。用单一全局 Agent 的判断替代仲裁 |
| **Agent 间对话 / 协商达成一致** | A1 原则 2 + A2 的"agent 间失配"类失败：分歧不会因为多轮对话而收敛，只会消耗上下文 |
| **durable execution 引擎（Temporal 类）** | 解决的是崩溃一致性，而"单写点 + 原子替换 + 幂等键"已覆盖 MVP 所需。**只借 determinism 作为测试思路** |
| **多 Agent 广搜**（除只读、独立、可复核的子任务） | A3 的收益依赖任务形状；WAM 的 Move 大多是写操作 |
| **statechart 代码生成 / 状态机框架库** | 我们只需要 `enum` + 6 条断言 + 1 个历史数组。引入运行时是把 20 行代码换成 2000 行依赖 |

---

## 4. 阅读顺序与时间盒（遵守 `reference/WORKFLOW.md`：每篇 ≤ 1 个会话）

| 顺序 | 读什么 | 为什么这个顺序 | 时间盒 | 何时读 |
|---|---|---|---|---|
| 1 | E1（停滞/自我评估偏差） | 它可能推翻 J6 的设计；越早越省 | 1 会话 | **W2 之前** |
| 2 | B1 SE-Blackboard | 决定 `directions/shared-context/` 的差异化表述是否诚实 | 1 会话 | W0–W1（不阻塞） |
| 3 | A2 MAST 的 14 种失败模式 | 变成 shared-context 的设计检查表 | 1 会话 | W2 之前 |
| 4 | B2 LLM 黑板 | 补全先例图谱 | 1 会话 | 之后 |
| 5 | D1 Harel（选读 §2–§3） | 已经用到了它的结论，读它是为了确保术语用对 | 0.5 会话 | W2 |
| 6 | E2 METR（读方法与图，不读全部） | 只取"任务时长"的量级 | 0.5 会话 | W3 |

**阅读不进入关键路径。** 唯一例外是 #1——它可能改变 J6，而 J6 在 W6 实现。**如果 W2 之前没读 #1，就不要在 W6 实现 J6，改为记一条 OQ。**

---

## 5. 对本文档的自我怀疑

| 怀疑 | 说明 |
|---|---|
| **"反多 Agent"的证据，主要来自工业界博客而非受控实验** | A1 是观点文（有说服力，但无实验）；A2 有数据但是**描述性**的（它说多 agent 会怎样失败，不说单 agent 一定更好）。所以 M6 的正确定位是"**有依据的拒绝 + 可证伪的例外**"，不是"已被证明的错误" |
| **最有价值的两条（E1、B1）都没读到全文** | 这是本会话最实际的不足。§4 的顺序就是为了还这个债 |
| **D3 是反例，我却继续推荐 10 个状态** | 我在 §2.D 给了理由，但那条理由没有证据。它在 W4 之后必须被检验：**作者是否真的看了第 6–10 个状态** |
| **"共享上下文"的差异化，可能只是命名差异** | 如果 B1/B2 读完后发现它们已经在做"多层级 + 显式探索边界"，那 `directions/shared-context/` 的贡献就只剩"拒绝仲裁器"这一点。**这不丢人，但要如实改写** |

---

## 6. 相关文档

| 需要 | 去看 |
|---|---|
| 每格的承诺与证据标准 | `docs/development/scope.md` |
| 这些材料在 9 周里什么时候用 | `docs/development/roadmap.md` |
| 共享上下文方向的假设与证伪 | `directions/shared-context/README.md` |
| 借鉴流程的正式规则 | `reference/WORKFLOW.md`、`reference/templates/assessment-matrix.md` |
| 已有的 5 篇入库文献 | `reference/README.md` |
