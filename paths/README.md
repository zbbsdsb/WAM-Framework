# Paths — 架构路径登记表

> 这里登记**整套架构的探索**，不是功能提案（功能提案在 `../directions/`）。
> 规则：[`../PATH_GOVERNANCE.md`](../PATH_GOVERNANCE.md)。**没有任何一条 Path 是默认的**——包括 `octsix`。

---

## 1. Registry

| id | 一句话主张（不是结论） | 状态 | 已晋升组件 | 关联实验 | 最后动作 |
|---|---|---|---|---|---|
| [`octsix/`](octsix/) | 用一个统一的智能协作主体承载六个候选空间：Intent / Shared Context / Cognition / Action / State / Reflection | **Proposed** | 无 | 无 | 2026-11-11 建立目录（作者口述，假设尚未写成可证伪形式） |

空表是正常的：**这个仓库目前只有一条被命名的 Path，且它还没有写下一个字。** 加第二条不需要改任何既有文件（见 §2）。

> 只有两列是状态：`状态` 与 `已晋升组件`。**不要在这里加"概念模型 / 组件分类 / 状态表示"之类的列**——那是 `comparison.md` 的事，把它做成登记表的列会强迫所有 Path 用同一套分类（`PATH_GOVERNANCE.md` §6）。

---

## 2. 怎么加一条新 Path（5 步，不改任何既有文件）

```bash
cp -r paths/_template paths/<id>        # ① 复制模板
```

1. 改 `paths/<id>/README.md`：一句话主张、状态 `Proposed`、**与 core 的差异**、与其它 Path 的关系。
2. 写 `paths/<id>/hypothesis.md`：一行假设 + 至少一条**证伪条件**。写不出证伪条件 = 它还只是名字。
3. 在本文件 §1 加一行。
4. **不改 `docs/`、不改 `paths/octsix/`、不改别人的 Path。**
5. 需要共享材料时，**链接到 `research/`**，不复制。

状态推进到 `Exploring` 的判据：`hypothesis.md` 里有证伪条件。

---

## 3. 现在只有一条 Path，为什么还要这一层

因为第二条 Path 出现时，**没有它就只能覆盖第一条**。代价不是多一个目录，是"曾经试过什么、为什么放弃"这件事没有地方记。

反过来说：如果 6 个月内这里还是只有 octsix，且 octsix 也没写下一个字——那说明"多路径"是想象，按 `PATH_GOVERNANCE.md` §9 退化掉这一层。**这一层同样需要被证伪。**

---

## 4. 与其它层的关系（一句话版）

| 你有 | 去 |
|---|---|
| 一套新的整体架构想法 | `paths/<新 id>/` |
| 一个机制 / 组件的改进想法 | `../directions/` |
| 一篇论文 / 一次调研 | `../reference/` · `../research/` |
| 一次要跑的验证 | `../experiments/<id>/`（README 里写 `path: <id>` 或 `direction: <id>`） |
| 已被采纳、要约束实现的 | `../docs/`（走晋升，见 PATH_GOVERNANCE §5） |
