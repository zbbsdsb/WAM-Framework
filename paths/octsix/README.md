# Path: `octsix`

> Status: **Proposed** · Opened: 2026-11-11 · Owner: 作者（ceaserzhao）
> **本目录目前只有这一页。** 没有 `hypothesis.md`、没有 `comparison.md`、没有架构——不是因为漏了，是因为它们还没被写下来（见 §5）。
> 规则：[`../../PATH_GOVERNANCE.md`](../../PATH_GOVERNANCE.md) · 登记：[`../README.md`](../README.md)

---

## 1. 一句话主张

> 用一个**统一的智能协作主体**承载六个候选空间：**Intent / Shared Context / Cognition / Action / State / Reflection**。
> ——作者原话（2026-11-11），此处照录，未改写。

原文同时明确：**空间的数量、边界、相互关系都可能变化。**

## 2. 与 core 的差异

**未建模。** 目前唯一的已知线索是"六个空间"这一条命名主张；它相对 `docs/` 现有架构**赌的是什么、不同在哪，没有任何文件写过**。

按 `PATH_GOVERNANCE.md` §1，这条 Path 因此停在 `Proposed`：有名字、有一句主张，但**没有可证伪的形式**，也没有与 core 的差异说明。

> 不许从 §3 的词面对照反推差异——那正是"看到同一个词就合并"的反面错误。

## 3. 概念模型

六个空间的名单（作者给定，顺序照抄）：

| 空间 | 作者给过的说明 | 仓库里已有内容 |
|---|---|---|
| Intent | — | `docs/vision.md` §4.1（同名概念） |
| Shared Context | — | `directions/shared-context/`（**机制方向，不同层**，见 §4） |
| Cognition | — | 无同名；语义上最近的是 `docs/vision.md` §4.3 Judgment |
| Action | — | 无同名；最近的是 `docs/vision.md` §4.4 Move |
| State | — | 无同名；最近的是 `docs/architecture.md` §8 Persistent Record / `StateRepository` |
| Reflection | — | 无同名；`docs/decisions/register.md` H-08（自动摘要/状态压缩）已拒绝进 MVP |

**这是词面对照，不是等价判断。** 上表只说明"仓库里有没有出现过相近的词"，不说明它们是同一个东西，也不说明六个空间应当替代或吸收这些概念。

**core 里有、而六个空间里没有的词**：`Situation`（`docs/vision.md` §4.2）、`Evidence`（§4.5）、`Move` 生命周期、注意力状态机（`docs/architecture.md` §12）。
**六个空间里有、而 core 里没有的词**：`Cognition`、`Reflection`、`State`（作为空间名）。

## 4. 关系

| 对象 | 关系 | 说明 |
|---|---|---|
| `directions/shared-context/` | **同名不同层，不合并** | 那边是"分层共享上下文 + 显式探索边界"的**机制假设**；这边是 OctSix 概念模型里的一个**空间**。按 `PATH_GOVERNANCE.md` §7，书写时必须带限定词 |
| `docs/`（canonical） | **未裁决（OQ-28）** | 见 §6 |
| 其它 Path | 暂无 | 本仓库目前只有这一条 |

## 5. 已晋升组件

无。

**注意**：`docs/` 里现有的一切（五概念、核心循环、6 接口、注意力状态机）**都不是从这条 Path 晋升来的**——它们先于这条 Path 被记录，且当时并未以 Path 的形式存在。它们的归属见 §6。

## 6. 未裁决：core 现在的内容，是 canonical 还是 OctSix 的前身？（OQ-28）

两种读法都成立，仓库无法自己判定：

| 读法 | 依据 | 若成立，后果 |
|---|---|---|
| **A. `docs/` 是 canonical** | 五概念、核心循环、6 接口都以 B 类（当前设计基线）登记在 `docs/decisions/register.md`，属于"已采纳" | OctSix 是一条**新**路径，要与 core 竞争；它需要写清差异 |
| **B. `docs/` 其实是 OctSix 的早期形态** | 作者 2026-11-11 的措辞是"六个空间**目前**是 OctSix 的探索，不能因为它们在当前路径里就变成 WAM 的强制顶层抽象"——这暗示当前写的这些东西，本就属于某条路径 | `docs/vision.md` §4、`docs/architecture.md` 的主体需要**降级**为 `paths/octsix/`，core 只剩 `foundation.md` 与尚未写出的通用部分 |

**在裁决之前，本仓库按 A 处理**（`docs/` 保持 canonical，OctSix 作为新路径登记）。理由：A 是可回退的（把文件搬进 octsix/ 是一次移动），B 是不可回退的（一旦把 canonical 降级，别人已经引用的"已采纳"就失效了）。**不确定时选可逆的那一边。**

这条 OQ 已登记在 `docs/decisions/register.md`。

## 7. Work log

- 2026-11-11：建立目录与登记行。状态 `Proposed`。没有写任何架构内容——作者只给了空间名单，没给假设、边界、判据。
- 2026-11-11：仓库内可查到的唯一 OctSix 痕迹是 `research/archive/raw-archive.md` B-288（`相关笔记/ceaser/WAM OctSix Topology.canvas`，334 B，节点仅"未命名组 / Ori Agent"）。**除此之外零内容。**

## 8. Next step

写 `hypothesis.md` 的第一行：**这六个空间要解决 core 解决不了的什么问题**，以及**什么观察会让它不成立**。

写不出来之前，不要写 `architecture.md`——先有假设，再有结构。
