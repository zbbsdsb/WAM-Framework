# Goals

> Goal tree. Each item: `- [ ] Title — Weight: critical path/enhancement/noise — Progress — Next step`
> Weight tiers: critical path (blocked without it) > enhancement (better with it) > noise (not done, not scheduled)

## M0 Foundation (current milestone)

- [x] Define the state model and collaboration protocol — Weight: critical path — Progress: done — Evidence: docs/01-foundation.md
- [x] Set up the four workspace/ state files and record the project founding — Weight: critical path — Progress: done — Evidence: this directory
- [x] Run a real session through the full six-step protocol (Read→Wait→Judge→Do→Verify→Write) — Weight: critical path — Progress: done — Evidence: all sessions 2026-08-06/07 followed the loop (bootstrap, README, translation, survey); this session: read→wait→judge→do(dispatch)→verify(results)→write

## M1 方向竞争与第一个切片（current next milestone）

- [x] Targeted survey: ecosystem / memory & state / unknown & weight — Weight: critical path — Progress: done — Evidence: docs/research/*
- [x] Establish directions/ folders + promotion gate (three tiers: evidence / proposals / decisions) — Weight: critical path — Progress: done — Evidence: directions/README.md, docs/01-foundation.md §Development Governance
- [x] Open 4 competing directions: global-route (author) / substrate / agent-plugin / weight-first — Weight: critical path — Progress: done — Evidence: directions/*/README.md
- [x] Public site: site/index.html (bilingual EN/中文, atompunk) — Weight: enhancement — Progress: done — Evidence: site/index.html, https://zbbsdsb.github.io/WAM-Framework/
- [x] M1 execution plan confirmed: substrate (stage 1, +verify-gate) / agent-plugin (stage 2) / weight-first (stage 3) slices; global-route minimal resume experiment; state-v2 deferred — Weight: critical path — Progress: done — Evidence: workspace/decisions.md
- [x] Reference library (reference/): 5 papers ingested, tiered critical/enhancement/noise with utilization explorations — Weight: enhancement — Progress: done — Evidence: reference/*
- [x] Reference library full documentation: every entry carries method/experiments/limitations/mapping/evaluation-criteria/R&D-path; site REFERENCE section (№ 06) live — Weight: enhancement — Progress: done — Evidence: reference/*.md, https://zbbsdsb.github.io/WAM-Framework/details.html
- [x] Scientific borrow-to-R&D workflow (reference/WORKFLOW.md): Ingest→Assess→Propose→Verify→Integrate→Revisit + assessment matrix template + anti-borrow list — Weight: enhancement — Progress: done — Evidence: reference/WORKFLOW.md, reference/templates/assessment-matrix.md
- [ ] Assess critical papers (survey, BMAM) via the matrix — Weight: enhancement — Progress: not started — Next step: after substrate stage 1 (assessment is AI-drafted, author-approved, no code)
- [ ] Dashboard P1: generator (scripts/dashboard.py) + Mission Control + Goals Board + Evidence Trail — Weight: enhancement — Progress: not started — Next step: after Stage 1 (shares its parser); DoD: renders from real workspace data, zero console errors, sampled cross-check passes — Evidence: docs/02-dashboard-plan.md
- [ ] Dashboard P2: Direction Races (needs Status: field in direction READMEs) + Decision Ledger + Reference Status + gate traffic lights — Weight: enhancement — Progress: not started — Next step: after P1; DoD: 6 panels, traffic lights match manual review on 5 samples
- [ ] Dashboard P3: deploy dashboard.html to gh-pages + nav entry — Weight: enhancement — Progress: not started — Next step: after P2; DoD: live URL + byte-identical sync + i18n intact
- [ ] Dashboard P4: parse/validate logic reused as substrate CLI state check — Weight: critical path — Progress: not started — Next step: with substrate stage 1
- [ ] Stage 1: substrate vertical slice — wam CLI (state check / goal next / log append) + evidence checker — Weight: critical path — Progress: not started — Next step: next session — LOCKED as the single next step (team confirmation 2026-08-15); DoD: catches a real format error in WAM's own workspace, answers "what's next" without reading files by hand, checker flags an evidence-less "done"
- [ ] Stage 2: agent-plugin vertical slice — a host-agent skill implementing the six-step protocol, used on the WAM repo for a week — Weight: critical path — Progress: not started — Next step: after the minimal verifiable core; DoD: skill's state check catches something the host agent would have missed in 3 consecutive sessions. NOTE 2026-10-09: was "stage 2 / Hermes skill"; platform term corrected (Hermes not found on this machine, DSH preset mechanism is the verified one) and ordering changed per docs/06-development-plan.md §1
- [ ] Stage 3: weight-first vertical slice — goal DAG + critical-path computation on goals.md — Weight: critical path — Progress: not started — Next step: after the minimal verifiable core; DoD: within two weeks the computed critical path changed or prevented a priority decision. NOTE 2026-10-09: placed **outside the MVP** per docs/06-development-plan.md §4 (dependency structure ≠ importance; P2)
- [ ] Global-route minimal resume experiment (cross-session "continue" from workspace/) — Weight: critical path — Progress: not started — Next step: promoted to MVP stage 2b per docs/06-development-plan.md §3.2, because "recover after interruption" is MVP capability #8; no full engine
- [x] Experiment track space established: experiments/ (governance README + _template with stage skeleton + DSH preset example) — Weight: critical path — Progress: done — Evidence: experiments/README.md, experiments/_template/*
- [ ] Design the first experiment path (hypothesis, stage list, DSH preset) — Weight: critical path — Progress: not started — Next step: discussion with author (next session)
- [ ] Convergence: first direction to pass the promotion gate defines M1 architecture; others archive or merge — Weight: critical path — Progress: not started

## M2 设计收敛与开发准备（2026-10-09 开启）

> 本节由 2026-10-09 的文档收敛任务产生。目标：把已有材料整理为一致、可追溯、适合正式开发的文档，并在收敛过程中如实标出未解决项。

- [x] 现状审计：仓库 / 文档 / 代码 / git 状态全量核查 — Weight: critical path — Progress: done — Evidence: docs/07-decision-register.md §5（已识别 5 项文档与现实不一致）；`git ls-files` 29 项、零实现代码；DSH preset 目录结构已对 `D:/github projects/deepseek-harness/apps/cli/config/agent-presets/` 核实
- [x] Vision & Core Concepts（docs/03）：问题定义、核心愿景、"WAM 没有自身渴望"前提、五核心概念、Judgment 六维度、七条设计原则、概念↔仓库词汇桥接 — Weight: critical path — Progress: done — Evidence: docs/03-vision-and-concepts.md
- [x] Architecture（docs/04）：核心循环、概念架构图、组件职责、五级证据阶梯、Persistent Record、执行层边界、Human Absent Mode、现有仓库映射 — Weight: critical path — Progress: done — Evidence: docs/04-architecture.md
- [x] State / Move / Evidence Model（docs/05）：Situation 必备内容、认识论五分、Move 生命周期与状态机、执行/验证/提交分离、失败信息、跨会话恢复核对 — Weight: critical path — Progress: done — Evidence: docs/05-state-move-evidence.md
- [x] Development Plan（docs/06）：最小可验证内核、两条阶段门、明确推迟项及理由、阻塞开发的 B1–B5、验证顺序 — Weight: critical path — Progress: done — Evidence: docs/06-development-plan.md
- [x] Decision Register（docs/07）：四态归类 13 条已确立 / 8 条基线 / 8 条假设 / 17 条开放问题 + 5 项文档与现实不一致 — Weight: critical path — Progress: done — Evidence: docs/07-decision-register.md
- [x] Scenarios & Acceptance（docs/08）：10 条通用行为验收 + 4 类设计验证场景（Kaggle / 论文复现 / 开源 / 社科）+ 检验设计自洽的方法 — Weight: critical path — Progress: done — Evidence: docs/08-scenarios-and-acceptance.md
- [x] 入口与过期标注：README 加文档地图与真实成熟度；docs/01-foundation.md 加指针（不改动 M0 内容）；directions/ 标注 Hermes 表述与 Sponge 口径冲突 — Weight: critical path — Progress: done — Evidence: README.md §Status/§Documentation map, docs/01-foundation.md, directions/*/README.md 顶部标注
- [ ] **作者裁决 OQ-09 / OQ-10**：WAM 与 Sponge 的关系；是否绑定执行平台 — Weight: critical path — Progress: not started — Next step: discussion with author. **已降级为不阻塞 MVP**（docs/06 §11.5：MVP 刻意不依赖任何未裁决的架构争议）
- [ ] **作者确认 OQ-01 / OQ-05 的初版设计**：Intent 最小表达与授权边界表达已由 docs/06 §5.2/§6.2 给出草案 — Weight: critical path — Progress: not started — Next step: author review of docs/06 §6.2 before T-04; 阻塞 T-04 之后的循环部分，不阻塞 T-01–T-03
- [x] **OQ-06b 已解决**：阶段技术选择定为 Python 3.13 + 零第三方依赖 — Weight: critical path — Progress: done — Evidence: docs/06-development-plan.md §1.2（stdlib 17/17 实测）、docs/07 B-09、X-05/X-07
- [ ] **P0-1 验证 codex 认证**（OQ-19） — Weight: critical path — Progress: not started — Next step: 在项目终端跑 `codex exec --ephemeral -s read-only "reply ok"`；不通则 I3/I4 换实现，接口已留好 — Evidence: 待补
- [ ] **MVP Phase 1：打通最小闭环（T-01→T-09）** — Weight: critical path — Progress: not started — Next step: T-01 工程骨架 → T-02 StateRepository → T-03 SituationBuilder → T-04 Intent+授权 → T-05 Move 结构 → T-06/07/08 执行器·验证器·Judgment → **T-09 竖切串起来（第一个里程碑）** — DoD: docs/06-development-plan.md §3.3 的 4 条判据 + §9.2 的 A1/A2/A11
- [ ] **MVP Phase 2：提高状态与证据可靠性（T-10→T-13）** — Weight: critical path — Progress: not started — Next step: 幂等与中断恢复、三条降级路径、失败信息回写 Situation、自动化测试套件 — DoD: docs/06 §9.2 的 A3–A9 + A12，其中 A6 必须在真实 kill 场景下验证
- [ ] **MVP Phase 3：固定接口与替换边界（T-14→T-15）** — Weight: enhancement — Progress: not started — Next step: Phase 2 之后再抽接口（先有真实实现，才知道边界在哪）；DoD: 抽取前后 `journal/` 序列逐字节相同 + 至少 1 个接口被假实现替换验证
- [ ] **MVP Phase 4：验证判断质量** — Weight: critical path — Progress: not started — Next step: 至少 2 个案例（含 1 个无数值指标）跑出完整闭环 + 失败分析；失败模式写进 docs/07 — Evidence: 待补
- [ ] **MVP fixture 项目**：`experiments/mvp-loop/`（已有部分代码 + 实验记录 + 一个已知未修问题） — Weight: critical path — Progress: not started — Next step: Phase 1 的验收对象；**不在 WAM 仓库自身 dogfood**（OQ-18 双权威冲突）
- [ ] **批次 0：验证与骨架**（P0-1 + T-01 + T-02） — Weight: critical path — Progress: not started — Next step: 待作者裁决第 1 项（codex 登录）后即可开工；T-01/T-02 本身无阻塞 — DoD: docs/06 §12.2（4 条测试全绿 + P0-1 有结论）
- [ ] **批次 1：三个数据结构**（T-03 + T-04 + T-05） — Weight: critical path — Progress: not started — Next step: 待作者裁决第 2、3 项（intent/authorization 结构、acceptance criterion 三类）；**不调用任何 LLM** — DoD: docs/06 §12.3（6 条测试全绿）
- [ ] **批次 2：执行器 + 验证器**（T-06 + T-07） — Weight: critical path — Progress: not started — Next step: 批次 1 之后；依赖 P0-1 结论 — DoD: docs/06 §12.4
- [ ] **批次 3：Judgment**（T-08） — Weight: critical path — Progress: not started — Next step: 批次 2 之后。**本批次最可能反复**；若调 3 次仍不稳则停止回设计（OQ-21） — DoD: docs/06 §12.5
- [ ] **批次 4：竖切 ★ 唯一里程碑**（T-09） — Weight: critical path — Progress: not started — Next step: 批次 3 之后 — DoD: docs/06 §12.6，其中判据 1（至少一次可验证的真实变化）为硬性
- [ ] **作者裁决清单**（docs/06 §13）：3 项阻塞（codex 登录 / intent+authorization 结构 / acceptance criterion 三类）+ 4 项建议 + 2 项 Phase 4 前回答 — Weight: critical path — Progress: **submitted for review 2026-10-09，待作者答复** — Next step: author review

## M3 目标分类学与 2027-01-01 路线（2026-10-28 开启）

> 本节由 2026-10-28 的 taxonomy + 路线任务产生。**执行细则以 `docs/10-rd-roadmap-2027.md` 为准**，本节只登记目标与状态，不复制周表。

- [x] **目标分类学（docs/09）**：三轴（职责层 L0–L5 / 承诺 G1–G5 / 证据 E1–E4）、35 个格子、MVP 由格子推导（20 IN + 3 MIN + 12 OUT）— Weight: critical path — Progress: done — Evidence: docs/09-goal-taxonomy.md
- [x] **九周路线（docs/10）**：W0 校准 → W4 竖切（唯一不可谈判的门）→ W9 冻结；每周退出条件均为 E1；固定砍单顺序 — Weight: critical path — Progress: done — Evidence: docs/10-rd-roadmap-2027.md
- [x] **外部资产评估（docs/11）**：A/B/C 三级核实、adopt/adapt/defer/reject 裁决、反借鉴清单 5 条增量、阅读顺序（E1 停滞文献排第一）— Weight: enhancement — Progress: done — Evidence: docs/11-external-assets.md
- [x] **交互表征定稿（docs/04 §12）**：注意力状态机 10 状态 / 6 模式，与 Move 生命周期正交，六条不变量；CLI 头部四问 — Weight: critical path — Progress: done — Evidence: docs/04-architecture.md §12、docs/07 B-16
- [x] **第五方向 shared-context**：分层共享上下文 + 显式探索边界 + 默认单 Agent；含三条证伪条件与一会话实验 — Weight: critical path — Progress: done — Evidence: directions/shared-context/README.md
- [x] **执行器选择修正（B-15）**：codex 登录正常但 API 地区受限（403），改 DSH headless 为主、人作兜底 — Weight: critical path — Progress: done — Evidence: docs/07 B-15 / X-10；本会话 `codex exec` 实测输出
- [ ] **W0 三个决策**（docs/10 §4）：D1 执行器（跑一次 `dsh --profile headless`）/ D2 U1 状态机是否进 MVP / D3 共享上下文是否进 MVP — Weight: critical path — Progress: **not started** — Next step: 跑 `dsh --profile headless "输出这一行 JSON：{\"ok\": true}"`；三条决策各记一条 decisions.md
- [ ] **读 arXiv:2607.25152（停滞/自我评估偏差）** — Weight: critical path — Progress: not started — Next step: **W2 之前**；未读则 W6 不实现 J6（OQ-27）
- [ ] **按 docs/10 执行 W1–W9** — Weight: critical path — Progress: not started — Next step: W1 = 骨架 + StateRepository + schema v1（含 `agent_state` / `scope`）— DoD: docs/10 §3 W1 行
- [ ] **作者裁决**：docs/10 §4 的 D1–D3 + docs/09 §3.2 的 MVP 类型声明（只主张 T1） — Weight: critical path — Progress: submitted 2026-10-28 — Next step: author review

## Scheduled follow-ups (not expanded before M1)

- Tooling for state files: format validation, quick queries
- Assistance mechanism for weight judgment
- Runtime and agent layer (language/architecture TBD)
- Whether the four validation scenarios in docs/08 are runnable against the MVP, or need capability the MVP will not have (docs/08 §5.1 defers this deliberately)
- Dashboard P1–P4 (docs/02): ordered after MVP Phase 2, per docs/06 §9.3
- Whether the six MVP interfaces survive contact with real Phase 4 cases (docs/06 §5)
