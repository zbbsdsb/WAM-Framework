# Repository Migration Plan — 迁移计划

> 日期：2026-11-10 · 基线：`main` @ `5155a38`（工作树有 10 改 + 14 未跟踪）
> 目标结构：[`REPOSITORY_ARCHITECTURE.md`](REPOSITORY_ARCHITECTURE.md) · 依据：[`REFACTORING_AUDIT.md`](REFACTORING_AUDIT.md)
> 原则：**能搬就不改；必须改的地方，改的是路径和状态标记，不是理论内容。**

---

## 0. 前置条件（未满足不动手）

| # | 条件 | 现状 | 谁做 |
|---|---|---|---|
| **G-0** | **先提交一次基线**，把 10 个已修改 + 14 个未跟踪路径落进 git | 未满足 | **作者**（或授权我提交）。理由：迁移要 `git mv` 一堆当前未跟踪的文件，与未提交改动叠加后无法单独回滚 |
| **G-1** | D-1：`directions/` 保留目录名 + 引入 `parked` | 未裁决 | 作者 |
| **G-2** | D-2：`docs/06` 拆出 §5–§7（整段移动、节号保留） | 未裁决 | 作者 |
| **G-3** | D-3：`workspace/` 四文件保持原样 | 建议「是」 | 作者 |
| **G-4** | 是否同步改 `site/details.html` 的"实时状态"表述（对外承诺） | 未裁决 | 作者 |

G-1/G-2 未批时，仍可执行**批次 C**（`research/`）与 `docs/` 内的纯改名——它们不触碰宪法词汇、不改任何主张。**批次 B 的拆分、批次 D 的方向状态，必须等裁决。**

---

## 1. Action 词汇

| Action | 含义 |
|---|---|
| MOVE | 换目录，文件名不变 |
| RENAME | 换文件名（可同时换目录） |
| SPLIT | 一份文件整段切成两份，**原文不动、节号不改** |
| MERGE | 两份合成一份，**说明合并依据与信息如何保留** |
| ARCHIVE | 移入归档位置并标 `superseded`/`frozen`，**不删** |
| KEEP | 位置不动（可能追加状态头或指针） |
| CREATE | 新建（必须有实际内容，不做空目录） |
| **REWRITE** | 保留文件、重写内容（**新增的动作类型**；现有六种都无法表达"同一份文件但重复内容要删"。仅用于 README / CONTRIBUTING / goals.md / site 状态区，且都在下文逐条说明改了什么） |

**没有任何 DELETE。** 全仓 42 篇 Markdown 全部保留，`raw-archive.md` 与 `directions/` 的历史一律不删。

---

## 2. 逐文件迁移表 — 根目录

| Current Path | New Path | Action | Reason |
|---|---|---|---|
| `README.md` | `README.md` | REWRITE | 删 §Status（4 份状态拷贝之一，已过期）、删 12 行文档地图（移到 `docs/README.md`）、删"29 tracked files"（K-07）。保留：定位、Why the name、哲学、三条阅读路径、站点链接 |
| `idea.md` | `idea.md` | KEEP | 起源文本，15 个文件引用它，动不了 |
| `rawnote.md` | `research/notes/rawnote.md` | MOVE | 作者脑暴材料 = 知识层；文件名保留（文件内标题与 49 处自引用都指 `rawnote`） |
| `raw-archive.md` | `research/archive/raw-archive.md` | MOVE + 修首行标题 | 3.5 MB 原文汇编 = 知识层归档。首行 `# rawnote.md —` 与文件名不符（K-12），改为实际文件名与日期 |
| `.gitattributes` | `.gitattributes` | KEEP + 追加一行 | 追加 `raw-archive.md -diff`：3.5 MB 单文件进 diff 会拖死任何 review |
| — | `.gitignore` | CREATE | 现无忽略规则，`.workbuddy/`（本机 agent 数据）一次 `git add -A` 就会被提交进公开仓库（P-05）。内容：`.workbuddy/`、`.wam/`、`__pycache__/`、`*.pyc`、`.DS_Store` |
| — | `CONTRIBUTING.md` | CREATE | **文档规则的唯一住处**：四层可信度、§3 判定顺序、规范状态条、晋升门三出口、什么不算完成（无证据 = 未完成） |
| `REFACTORING_AUDIT.md` | 同左（评审期）→ 评审后 `research/archive/refactor-2026-11/` | KEEP（临时） | 重构过程记录属证据层；评审期放根目录便于阅读，评审后归档，并在 `docs/README.md` 留一行指针 |
| `REPOSITORY_ARCHITECTURE.md` | 同上 | KEEP（临时） | 同上 |
| `REPOSITORY_MIGRATION_PLAN.md` | 同上 | KEEP（临时） | 同上 |
| `REFACTORING_REPORT.md` | 同上 | KEEP（临时） | Phase 5 产出 |

> 四份报告顶部各加一行：`> 路径为 2026-11 迁移前状态；迁移后位置见 docs/README.md`。它们描述的是旧结构，不改写（F：可追溯）。

---

## 3. 逐文件迁移表 — `docs/`

| Current Path | New Path | Action | Reason |
|---|---|---|---|
| `docs/01-foundation.md` | `docs/foundation.md` | RENAME | 去掉序号（P-02：编号 = 写作顺序）。它是宪法，位置应在 docs 根 |
| `docs/02-dashboard-plan.md` | `docs/development/dashboard-plan.md` | MOVE + 顶部加状态条 | 计划类，且**已推迟**（`docs/10 §7`）。正文不动，只加：`Status: deferred — 九周内不做；重开条件见 roadmap §7`。修 K-04/K-05 里它仍在推销"4 方向 + 立即开工"的部分**不做删改**，状态条使其失效 |
| `docs/03-vision-and-concepts.md` | `docs/vision.md` | RENAME | 名实一致（`vision-and-concepts` → `vision`，概念仍在正文 §4） |
| `docs/04-architecture.md` | `docs/architecture.md` | RENAME | 架构的唯一住处；不拆（§10 触发条件） |
| `docs/05-state-move-evidence.md` | `docs/specifications/state-and-evidence.md` | MOVE + 状态条 | 它已是规范（Situation 必备内容 / 认识论五分 / Move 生命周期 / 恢复判据），错在放在 docs 根 |
| `docs/06-development-plan.md` §5–§7（第 232–549 行：`## 5.` 起，至 §7 最后一行止；550–551 行是分隔线与空行，留在原地） | `docs/specifications/execution-contract.md` | **SPLIT** | 接口 / `state.json` schema / Move 生命周期 = 契约，不是计划。**整段 318 行原文照搬，节号 §5/§6/§7 原样保留**，因此 15 个文件里 27 处 `docs/06 §5.x` 只需换路径、不必换节号 |
| `docs/06-development-plan.md` 剩余（§0–§4 + §8–§15） | `docs/development/mvp-plan.md` | MOVE + 切口指针 | 环境基线 / 能力分级 / 任务 / 阶段门 / 批次（已被 roadmap 取代）/ 自评。在 §4 与 §8 之间插入一行：`> §5–§7 已移至 docs/specifications/execution-contract.md（原文与节号未改）`。**保留 §12 的历史批次段**（它自己已标"保留为历史记录"） |
| `docs/07-decision-register.md` | `docs/decisions/register.md` | MOVE | 决策状态索引；事件流水仍在 `workspace/decisions.md`（双文件规则写进 CONTRIBUTING） |
| `docs/08-scenarios-and-acceptance.md` | `docs/specifications/acceptance.md` | MOVE + 状态条 | 10 条行为验收 + 4 类场景 = 验收契约 |
| `docs/09-goal-taxonomy.md` | `docs/development/scope.md` | MOVE | 范围权威（36 格 / MVP 推导）。不是规范、不是架构，是"做不做" |
| `docs/10-rd-roadmap-2027.md` | `docs/development/roadmap.md` | MOVE | 时间唯一权威 |
| `docs/11-external-assets.md` | `research/external-assets.md` | MOVE | 外部工作核实 + 取舍 = 知识层（不是我们的决定） |
| `docs/research/01-ecosystem-survey.md` | `research/briefs/01-ecosystem-survey.md` | MOVE | 证据层从规范性目录里搬出（P-03） |
| `docs/research/02-memory-and-state.md` | `research/briefs/02-memory-and-state.md` | MOVE | 同上 |
| `docs/research/03-unknown-and-weight.md` | `research/briefs/03-unknown-and-weight.md` | MOVE | 同上 |
| — | `docs/README.md` | CREATE | **唯一文档地图**：每份文档一行"它回答什么问题 / 什么时候读 / 当前状态"。取代 README 里的 12 行表格 |
| — | `research/README.md` | CREATE | 写清 `research/` 与 `reference/` 的边界（外部论文 = `reference/`，我们的调研与作者材料 = `research/`），否则一年后必然重复 |

`docs/` 拆分后不再有编号前缀。**这是唯一会让 15 个文件里 46 处 `docs/06-…` 引用失效的动作**，替换规则见 §6。

---

## 4. 逐文件迁移表 — `directions/`（D-1 裁决后执行）

| Current Path | New Path | Action | Reason |
|---|---|---|---|
| `directions/README.md` | 同左 | REWRITE（治理段） | 加第三个出口 `parked`（审计 P-06）；三层信任表不变 |
| `directions/shared-context/README.md` | 同左 | KEEP + 加 `Status:` 头 | 唯一 active；下一步指向将来的 `experiments/shared-context-scope-conflict/` |
| `directions/global-route/README.md` | 同左 | KEEP + 加 `Status: parked` 段 | 已被两处吸收：resume 能力 → `mvp-plan §3.2`；单一全局实体 → `shared-context §5`。**不归档**：它没被证伪，只是被吸收 |
| `directions/substrate/README.md` | 同左 | KEEP + `Status: parked` | 它的第一刀就是 `roadmap` W1；以任务形式继续，不以方向形式 |
| `directions/agent-plugin/README.md` | 同左 | KEEP + `Status: parked（冲突未解）` | 与 `shared-context §8` 明确互斥（scope 归谁分配）。这是**未解决的设计冲突**，不允许被归档抹平 |
| `directions/weight-first/README.md` | 同左 | KEEP + `Status: parked（MVP 已拒绝，方向未证伪）` | `docs/09` H-04 → G5、`roadmap §7` 明确不做；但"依赖结构 ≠ 重要性"只是拒绝理由，不是证伪 |
| `directions/archive/architecture/README.md` | 同左 | KEEP | 已归档（2026-08-07 被四方向取代），有决策依据 |

> 为什么**不移动**这四个目录：`directions/` 被 24 个文件引用 117 处，其中大量是 `raw-archive.md` 里不可改写的原文。移动只带来引用成本，不带来任何信息增益。**加状态头即可让读者一眼看到"这不是现在在做的事"。**

---

## 5. 不动的部分（KEEP 全量）

| 路径 | 理由 |
|---|---|
| `workspace/{state,goals,log,decisions}.md` | M0 宪法条文（四文件）。**位置不动、文件不拆。** 内容按协议追加（见 §7） |
| `experiments/` 全部 9 个文件 | 结构已对（README 规程 + `_template` + `archive/`）；0 条路径，无需三分布局 |
| `reference/` 全部 8 个文件 | 自带六阶段流程 + 评估模板 + 三档权重，是外部论文的唯一住处 |
| `site/index.html` · `site/style.css` | 公开页与设计系统；路径不动（gh-pages 同步流程依赖它，`log.md:17` 记录过这个坑） |
| `site/details.html` | 结构不动；**仅改 LIVE STATUS 区**（G-4 裁决后）：把"mirrors workspace"改成"frozen snapshot 2026-08-07"，或整段删除。**不改设计、不重排版** |

---

## 6. 引用修复清单

### 6.1 路径映射（脚本用；顺序敏感，长的在前）

```text
docs/06-development-plan.md   → docs/development/mvp-plan.md        （§5–§7 部分 → docs/specifications/execution-contract.md）
docs/05-state-move-evidence.md → docs/specifications/state-and-evidence.md
docs/08-scenarios-and-acceptance.md → docs/specifications/acceptance.md
docs/07-decision-register.md  → docs/decisions/register.md
docs/09-goal-taxonomy.md      → docs/development/scope.md
docs/10-rd-roadmap-2027.md    → docs/development/roadmap.md
docs/02-dashboard-plan.md     → docs/development/dashboard-plan.md
docs/11-external-assets.md    → research/external-assets.md
docs/04-architecture.md       → docs/architecture.md
docs/03-vision-and-concepts.md → docs/vision.md
docs/01-foundation.md         → docs/foundation.md
docs/research/                → research/briefs/
rawnote.md                    → research/notes/rawnote.md
raw-archive.md                → research/archive/raw-archive.md
```

同时要处理的三种引用形式：

| 形式 | 例 | 处理 |
|---|---|---|
| Markdown 相对链接 | ``[docs/06](docs/06-development-plan.md)``、``[../docs/07](../docs/07-decision-register.md)`` | 改路径；**相对层级变化的要重算 `../`**（如 `directions/*/README.md` 引用 `../docs/06`，目标没深层变化；`research/briefs/*` 引用 `../../docs/…`） |
| 行内反引号路径 | `` `docs/06 §5.2` `` | 只换路径，节号保留 |
| `文件:行号` | `rawnote.md` 的 49 处 `docs/04:538` | **只换路径前缀**，行号不动（本次迁移不重排任何文件内容，行号在纯移动下不变） |

### 6.2 需要改引用的文件（12 个）

`README.md` · `docs/01-foundation.md` · `docs/03` · `docs/04` · `docs/05` · `docs/06` · `docs/07` · `docs/08` · `docs/09` · `docs/10` · `docs/11` · `docs/research/*` · `directions/**`（6 个）· `reference/README.md` · `reference/WORKFLOW.md` · `workspace/{state,goals,log,decisions}.md` · `experiments/README.md` · `rawnote.md`

**不改**：`raw-archive.md`（原文照录，改了就不是原文了）。

---

## 7. `workspace/` 的四条内容更新（协议要求，非结构改动）

| 文件 | 改什么 | 为什么不算"改写理论" |
|---|---|---|
| `state.md` | ① 修第 11 行 `four competing directions` → 五（K-05）；② 追加一条 2026-11-10 结构重构记录 | ① 是事实纠错；② 是协议规定的会话收尾 |
| `goals.md` | 只保留「目标 — 权重 — 状态 — 证据」；把**三代已作废的待办**（Dashboard P1–P3、`Stage 1 LOCKED`、批次 0–4、P0-1）移入文件末尾 `## 已作废（历史，不删）` 段并各注一句作废原因 | 不删任何条目；作废原因指向取代它的文档。这是执行「一个事实一个住处」的必要动作 |
| `log.md` | 追加 2026-11-10 条目（含证据：迁移前后树、链接检查输出） | 协议 |
| `decisions.md` | 追加一条：`[2026-11-10] 仓库结构重构`（理由 / 替代方案 / 权重） | 协议；同时登记到 `docs/decisions/register.md` |

---

## 8. 执行批次（每批一个 commit，可独立回滚）

| 批次 | 内容 | 依赖 | 验证 |
|---|---|---|---|
| **A 前置** | 作者提交基线；`CREATE` `.gitignore`；四份报告落根 | G-0 | `git status` 干净 |
| **B `docs/` 归位** | 9 个 RENAME/MOVE + 1 个 SPLIT + `docs/README.md` + 引用修复 | G-2 | §9 的 5 项检查 |
| **C 知识层** | `research/` 建立（4 个 MOVE + 1 README） | 无 | 链接检查 |
| **D 提案层与入口** | `directions/` 状态头 + `workspace/` 四条更新 + `README.md`/`CONTRIBUTING.md` 重写 | G-1 | 人工读一遍三条路径是否通 |
| **E 收尾** | `site/details.html` 状态区（G-4）+ 四份报告归档 + `REFACTORING_REPORT.md` | G-4 | 全仓检查 |

**顺序理由**：B 最痛（引用密集）先做完；C 独立无依赖；D 只追加状态，风险最低但需要裁决；E 属对外承诺，最后做。

---

## 9. 验证方式（每条都要有输出）

| # | 检查 | 命令 / 方法 | 通过标准 |
|---|---|---|---|
| V-1 | 无断链 | 脚本解析全部 `.md` 相对链接，**排除 `research/archive/raw-archive.md`** | 0 条（基线也是 0，见审计 §0） |
| V-2 | 无旧路径残留 | `grep -rn "docs/0[1-9]-\|docs/10-rd\|docs/11-external\|docs/research/" --exclude-dir=.git --exclude=raw-archive.md .` | 仅命中四份重构报告（它们描述旧状态，允许） |
| V-3 | 拆分无内容丢失 | 把新 `execution-contract.md`（去头部）+ `mvp-plan.md`（去插入行与追加头）按原顺序拼接，与 `git show HEAD:docs/06-development-plan.md` 做 `diff` | 除头部与切口注记外**逐字节相同** |
| V-4 | 行号引用仍有效 | 抽查 `rawnote.md` 的 5 处（02/04/06 各若干），按新路径取对应行 | 内容语义一致（纯移动下行号不变） |
| V-5 | 目录无空壳 | `find . -type d -empty -not -path "./.git/*"` | 0 个（除 `experiments/archive/`，它已有 `.gitkeep`） |
| V-6 | README 与实际一致 | 人工对照 `docs/README.md` 表格 vs `find docs -name "*.md"` | 一一对应 |
| V-7 | 状态唯一性 | 搜 `M1\|M2\|M3\|W0\|W4\|current stage\|Current stage` 在 `README` 与 `site/` 的出现 | README 0 处状态复述；site 只留 frozen 标注 |

---

## 10. 回滚

- 每批一个 commit ⇒ `git revert <sha>` 即可。
- SPLIT 的回滚成本最低（原文件在 git 历史里完整存在，`git show` 可取回）。
- **禁止**用 `git reset --hard` 回滚（会连带丢掉未提交的 rawnote/raw-archive）。

---

## 11. 本次迁移不做的事（明确写下，防止扩张）

1. 不改任何理论内容：不合并冲突（K-01/K-09 保留）、不裁决 OQ、不动 `directions/*` 的正文论证。
2. 不写任何实现代码，不建 `src/` `tests/`（W1 的 T-01 才建）。
3. 不重排 `docs/06` 的章节顺序（保行号）。
4. 不修 `raw-archive.md` 的 33 处内部链接（它是原文汇编）。
5. 不改 `site/` 的设计与结构，只动一句状态表述。
6. 不新建术语表 / 索引页 / 看板等派生文档。
7. 不提交 `site/` 到 gh-pages（无凭证；需作者在自己终端 push）。
