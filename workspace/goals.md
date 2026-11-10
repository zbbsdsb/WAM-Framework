# Goals

> 规则：本文件只记「目标 — 权重 — 状态 — 证据」。
> **计划**（什么时候做）以 [`docs/development/roadmap.md`](../docs/development/roadmap.md) 为唯一权威；**范围**（做不做）以 [`docs/development/scope.md`](../docs/development/scope.md) 为准。
> 本文件**不复制**周表、批次、任务清单——2026-11-10 之前它同时挂着三代计划（Stage 1–3 / MVP Phase 1–4 / 批次 0–6 / W0–W9），结果四份都在过期。
> 权重档：critical path（没有它就走不动）> enhancement（有更好）> noise（不做，不排期）。**无证据 = 未完成。**

## 当前里程碑 — M3：2027-01-01 之前交付 MVP

- [x] **目标分类学**（`docs/development/scope.md`）：三轴（L0–L5 / G1–G5 / E1–E4）、**36 个格子**、MVP 由格子推导（20 IN + 3 MIN + **1 SEAM** + 12 OUT）— Weight: critical path — Evidence: docs/development/scope.md §2/§4
- [x] **九周路线**（`docs/development/roadmap.md`）：W0 校准 → W4 竖切（唯一不可谈判的门）→ W9 冻结；每周退出条件均为 E1；固定砍单顺序 — Weight: critical path — Evidence: docs/development/roadmap.md
- [x] **外部资产评估**（`research/external-assets.md`）：A/B/C 三级核实、adopt/adapt/defer/reject 裁决、反借鉴清单 5 条增量 — Weight: enhancement — Evidence: research/external-assets.md
- [x] **交互表征定稿**（`docs/architecture.md` §12）：注意力状态机 10 状态 / 6 模式，与 Move 生命周期正交，六条不变量；CLI 头部四问 — Weight: critical path — Evidence: docs/architecture.md §12、docs/decisions/register.md B-16
- [x] **第五方向 shared-context**：分层共享上下文 + 显式探索边界 + 默认单 Agent；三条证伪条件与一会话实验 — Weight: critical path — Evidence: directions/shared-context/README.md
- [x] **执行器选择修正（B-15）**：codex 登录正常但 API 地区受限（403），改 DSH headless 为主、人作兜底 — Weight: critical path — Evidence: docs/decisions/register.md B-15 / X-10
- [x] **仓库结构重构（2026-11-10）**：docs 按生命周期重排、`docs/06` 拆出规范段、`research/` 设层、方向加状态出口、建立唯一文档索引 — Weight: critical path — Evidence: REFACTORING_REPORT.md · docs/README.md
- [ ] **W0 三个决策**（`docs/development/roadmap.md` §4）：D1 执行器（跑一次 `dsh --profile headless`）/ D2 U1 状态机是否进 MVP / D3 共享上下文是否进 MVP — Weight: critical path — Progress: **not started（W0 窗口 10-28→11-01 已过）** — Next step: 跑 `dsh --profile headless "输出这一行 JSON：{\"ok\": true}"`；三条各记一条 decisions.md
- [ ] **按 `docs/development/roadmap.md` 执行 W1–W9** — Weight: critical path — Progress: **not started（W1 窗口 11-02→11-08 已过，仓内仍无 `.py`）** — Next step: W1 = 骨架 + `StateRepository` + schema v1（含 `agent_state` / `scope`）— DoD: roadmap §3 W1 行
- [ ] **读 arXiv:2607.25152**（停滞 / 自我评估偏差）— Weight: critical path — Progress: not started — Next step: **W2 之前**；未读则 W6 不实现 J6（OQ-27）
- [ ] **作者裁决**：`roadmap` §4 的 D1–D3 + `scope` §3.2 的 MVP 类型声明（只主张 T1）+ OQ-09 / OQ-10 — Weight: critical path — Progress: submitted 2026-10-28，待作者答复
- [ ] **第一个实验路径**：`directions/shared-context/` §6 的三阶段 scope 冲突实验（进 `experiments/`，不写产品代码）— Weight: enhancement — Progress: not started — Next step: 先读 SE-Blackboard（IEEE 11527206）

## M0 — 地基（已完成，证据保留）

- [x] 定义状态模型与协作协议 — Weight: critical path — Evidence: docs/foundation.md
- [x] 建立 `workspace/` 四文件并记录立项 — Weight: critical path — Evidence: workspace/
- [x] 用完整六步协议跑过一次真实会话（Read→Wait→Judge→Do→Verify→Write）— Weight: critical path — Evidence: 2026-08-06/07 各会话

## M1 / M2 — 已完成的历史目标（证据保留）

- [x] 定向调研：生态 / 记忆与状态 / 未知与权重 — Evidence: research/briefs/*
- [x] 建立 directions/ 与晋升门（三层信任：证据 / 提案 / 决策）— Evidence: directions/README.md、docs/foundation.md §Development Governance
- [x] 公开站点（双语，atompunk）— Evidence: site/index.html、https://zbbsdsb.github.io/WAM-Framework/
- [x] 借鉴库 `reference/`：5 篇论文入库、三档权重、六阶段借鉴流程 — Evidence: reference/*
- [x] 设计基线：vision / architecture / specifications / decisions / acceptance — Evidence: docs/
- [x] 工程计划：6 接口、`state.json`、15 个任务、阶段门、12 条验收用例 — Evidence: docs/development/mvp-plan.md
- [x] 实验路径空间 `experiments/`：宣言 + 生命周期 + DSH preset 机制 — Evidence: experiments/README.md

## 待作者裁决（仍开着，不属"作废"）

- **OQ-09** WAM 与 Sponge 的关系（外部口径冲突）— 见 `docs/decisions/register.md`；刻意不阻塞 MVP
- **OQ-10** 是否绑定执行平台 — 见 `docs/decisions/register.md`
- **D1 / D2 / D3**（`roadmap` §4）：执行器 / U1 状态机 / 共享上下文是否进 MVP

## 已作废（历史，不删）

> 每条写明"被谁取代"。删掉会让下一次会话把同一件事重新争论一遍。

- [ ] Dashboard P1–P4（`docs/development/dashboard-plan.md`）— 取代：`roadmap` §7 九周内不做；P4 的 `state check` 并入 W1
- [ ] Stage 1 substrate 竖切（2026-08-15 "LOCKED as the single next step"）— 取代：内容即 `roadmap` W1，任务形态取代方向形态
- [ ] Stage 2 agent-plugin / Stage 3 weight-first 竖切 — 取代：`scope` 判其不进 MVP（weight-first 见 H-04）；agent-plugin 已标 parked
- [ ] Global-route 最小 resume 实验 — 取代：并入 MVP 第 8 项能力（`mvp-plan` §3.2）
- [ ] Convergence：第一个通过晋升门的切片定义 M1 架构 — 取代：改为 `roadmap` W4 竖切；方向竞争改为 parked，不再"赛马"
- [ ] **P0-1 验证 codex 认证** — 取代：已证伪（认证通过、地区 403），见 B-15 / X-10
- [ ] MVP Phase 1–4（T-01→T-15 分四阶段）— 取代：`roadmap` W1–W9 时间化
- [ ] 批次 0–4（7 批次计划）— 取代：同上；`mvp-plan` §12 保留为历史
- [ ] MVP fixture 项目 `experiments/mvp-loop/` — 取代：`roadmap` W3 自带 fixture，路径未定
- [ ] 作者裁决 OQ-01 / OQ-05 初版设计 — 取代：草案在 `mvp-plan` §6.2，随 W2 实做后再定

## Scheduled follow-ups（不早于 W4）

- 状态文件工具化：格式校验、快速查询（= W1 的 `StateRepository`）
- 权重判断的辅助机制
- 运行时与 agent 层（语言 / 架构待定）
- `docs/specifications/acceptance.md` 的四个场景能否对 MVP 跑得动（§5.1 故意推迟）
- 6 个接口能否经受 Phase 4 的真实案例（`docs/specifications/execution-contract.md` §5）
