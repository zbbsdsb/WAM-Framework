# research/notes/rawnote.md — WAM 脑暴笔记

开会用。每张卡：一个现场、一句原话、一处卡住、一个待吵的问题。

出处写法：`docs/architecture.md:538` = `WAM Framework/docs/architecture.md` 第 538 行；`相关笔记/WAM/…` 与 `The-Throes/…` 在 `D:/github projects/OITS Repo/The-Throes/` 下。

---

## 1 现场

### 卡 1 · 用户只说了一句

用户：「帮我继续推进这个项目。」`docs/development/mvp-plan.md:159`

第一屏：

```
在做：     判断「先修失败测试还是先补实验记录」（第 3 次循环）
为什么：   引用 f2「pytest 3 个失败」+ a1「依赖回退」未验证
在等谁：   你
解锁动作： 确认 a1 是否为真 —— 这决定下一步是修 lockfile 还是查代码
```
`docs/architecture.md:538-541`

原话：「**在等时间** / **在等你**（两者必须分开说）」`docs/architecture.md:491`

原话：「把两者合成"等待中"会让用户不知道该不该回来——这正是 Continuity 失败的具体形态。」`docs/architecture.md:494`

卡住：用户回一句「你看着办」。

待吵：「在等你」改不改？改成「在等时间」就自己往下跑？

---

### 卡 2 · 执行器说完成

输入：执行器报告「完成」，实际产物或测试不支持。`docs/specifications/acceptance.md:66`

原话：「**Agent 自己声称"完成了"不等于事情已经完成。**」`docs/vision.md:181`

原话：「执行器报告成功 ≠ 完成 / 须取可检查证据」`docs/architecture.md:41`

原话：「| 2. 执行器报告成功 | 执行器 | **低——这是最常见的误判来源** |」`docs/architecture.md:212`

卡住：Evidence Trail 上已经挂了「✅ verified / ⏳ pending / ❌ failed」`docs/development/dashboard-plan.md:52`。

待吵：点开 evidence ref：「假执行器返回成功但产物不存在」`docs/development/mvp-plan.md:272`。徽章改成 ❌，还是先挂 ⏳？

---

### 卡 3 · 72 小时后回来

第一屏：「在等谁：你」「批准 sandbox 升到 workspace-write，或改 Move 为只读核验」`docs/architecture.md:519`

原话：「这条路径已停，理由是…」`docs/architecture.md:492`

原话：「**WAM 目前不具备 Human Absent Mode 的能力。** 本文档描述的是设计要求。」`docs/architecture.md:398`

原话：「把它做成状态会让"系统没在跑"看起来像"系统在工作"」`docs/architecture.md:553`

卡住：72 小时里没人点批准。

待吵：第一屏放哪句？「在等你」还是「这条路径已停，理由是…」？

---

### 卡 4 · 白板上的三种颜色

白板节点：「黄色 = 用户提示词 / 红色 = Agent的行动 / 蓝色 = Agent的生成物」`相关笔记/WAM/WAM Topology.canvas:17`

白板节点：「你的任务是参加ARC-AGI-3比赛，我准备好了Kaggle相关的令牌和设备，也规定了工作区」`相关笔记/WAM/WAM Topology.canvas:18`

白板节点：「AI进行项目的初始化」`相关笔记/WAM/WAM Topology.canvas:19`

分组：「Stage 1 初始化」「Stage 2 进行式循环」「Stage 3」`相关笔记/WAM/WAM Topology.canvas:8,9,7`

白板节点：「Master Agent」「Worker Agent」`相关笔记/WAM/WAM Topology.canvas:11,12`

白板节点：「架构不够Self-Aware」「需要翻阅90年代的文章（符号时期）」「自我感知数据库」「Multi-Agent 的调度问题」`相关笔记/WAM/WAM 的启发法设计_10_22.canvas:3,9,10,12`

卡住：「WAM不使用传统的Multi-Agent路径，」「WAM在默认的调度模式下只会启用Miracle Agent（也就是全局Agent），」`The-Throes/2026-10-27.md:10,19`

待吵：Master / Worker 两个节点，改名、合并，还是删掉？「架构不够Self-Aware」归到哪条边？

---

### 卡 5 · 复盘会

会议原话：「Retro (复盘会) | Goals Board vs Evidence Trail: did we do what we said? Where are the failures?」`docs/development/dashboard-plan.md:76`

原话：「活动量、生成内容、任务数都不能当进展」`docs/vision.md:250`

原话：「**WAM 不制造伪指标**（如把"完成度百分比"当成功标准）」`docs/specifications/acceptance.md:145`

原话：「**T10 是最难的一条**」`docs/specifications/acceptance.md:288`

卡住：「WAM 没有一个天然分数能够代表研究质量。」`docs/specifications/acceptance.md:253`

待吵：没有分数的项目，复盘会上看哪几行？

---

## 2 作者写下的话

- 「You ask in one paragraph, it answers in one paragraph」`idea.md:15`
- 「wait — do we really understand what the user wants? Do we really understand the current situation? Do we really know what the next step should be?」`idea.md:90`
- 「If we don't, don't rush to answer.」「Go figure it out first.」`idea.md:92,94`
- 「我最开始为什么想设计WAM这个框架」`相关笔记/ceaser/WAM框架和海绵设计哲学.md:1`
- 「在多个地方留下"自由容器"」`相关笔记/ceaser/WAM框架和海绵设计哲学.md:4`
- 「这些自由容器并没有固定的类型，可以是插件，也可以是可以由AI自由掌控，更改Pipeline的空间（我们正式把这种空间命名为AgentPark），」`相关笔记/ceaser/WAM框架和海绵设计哲学.md:8`
- 「在Sponge的切片里，用户可以在研究空间」（句子断在这里）`相关笔记/ceaser/WAM框架和海绵设计哲学.md:21`
- 「### WAM和Sponge的关系」下面只剩「经过之前许多天的头脑风暴」`相关笔记/ceaser/WAM框架和海绵设计哲学.md:50-52`
- `相关笔记/WAM/WAM的术语说明.md`：0 字节
- 「我前几天重新想起了搁置已久的WAM框架（并不是有意为之，而是需要Sponge做基础），」`相关笔记/ceaser/Diary/2026-09-15.md:33`
- 「为了让Sponge从一开始就十分好用，我们正在开发WAM Framework。」`相关笔记/ceaser/Diary/2026-09-16.md:22`
- 「我决定在2027年1月1日之前完成WAM的MVP，」`The-Throes/2026-10-27.md:7`
- 「我的新决策方法：3天一个周期，看打分，至于分怎么打，就全看打分时的心情了（1-10分）」`The-Throes/2026-10-15.md:4`
- 「WAM将不会引入一个"提示词编写Agent"（6分）」`The-Throes/2026-10-15.md:6`
- 「为WAM框架引入"初始回钩"的机制」`The-Throes/2026-10-19.md:17`
- 「把轨迹作为一种新的查看模式，添加到现有的显示模式，切换栏里面就相当于以后就有四种查看模式」`The-Throes/2026-10-15.md:9`
- 「我们想做成树状的，但是不知道怎么才能很好的把学习给表征出来」`The-Throes/2026-10-15.md:12`
- 「我突然想创办一个新公司，叫做CHORD，我花了一节课写完了CHORD 公司简章：」`The-Throes/2026-11-05.md:24`
- 「然后他露出了一副醍醐灌顶的表情，说：」「我在想，什么时候显性化边界之外的东西可以被人理解，什么时候不能，」`The-Throes/2026-11-05.md:17-19`
- 「the team's "不知所措" (lost feeling) is not a missing plan but the absence of any running artifact」`workspace/log.md:24`
- 「the one thing that had been "verified" (codex) had only had its *flags* verified, never an execution」`workspace/log.md:29`
- 「the plan is now 896 lines, which is longer than the 1% principle it cites」`workspace/log.md:31`
- 「Verified, not assumed.」`workspace/decisions.md:22`
- 「WAM（Wait a Minute）是一个面向跨对话、长周期复杂任务的人机协作 Agent Framework。」`相关笔记/CHORD/CHORD 公司简章.md:24`
- 「用户可以在里面使用封装后的WAM，CHORD的资料库，也有属于自己的Workspace。」`相关笔记/CHORD/CHORD 公司简章.md:19`
- 「注（给孙一楷）：我准备这个文章部署到github io的路由/whylemma，就从最朴素的结构主义风格，不要任何多余的装饰，这只会拉低我们的严肃性和信息密度。」`相关笔记/Lemma AI/Y Lemma.md:64`

---

## 3 卡在哪

| 卡点 | 原话 | 出处 |
|---|---|---|
| 判断没有载体 | 「**Judgment 无载体，Intent 无载体**」 | `docs/vision.md:240` |
| 用户意图没被记 | 「用户每次会话表达的意图与授权范围**完全没有被记录**」 | `docs/vision.md:233` |
| 零实现 | 「the implementation count is still zero, and that is now the project's main risk」 | `README:54` |
| codex 不可用 | 「codex-cli is logged in but `api.openai.com` is geo-blocked from this network」 | `README:54` |
| 计划比 1% 原则长 | 「the plan is now 896 lines」 | `workspace/log.md:31` |
| W4 是唯一的门 | 「**只有 W4 是不可替换的。**」 | `docs/development/roadmap.md:91` |
| 字段没人读 | 「scope 字段加了，但**从未被任何代码读取过**」 | `directions/shared-context/README.md:38` |
| 失败只影响进度条 | 「失败信息没有进入 Situation，Judgment 的输入没变」 | `docs/specifications/state-and-evidence.md:210` |
| 无指标仍要推进 | 「判断的可信度不来自数字，而来自"理由 + 证据 + 认识论状态"」 | `docs/specifications/acceptance.md:144` |
| 判断没测过 | 「**Judgment 质量完全未测**」 | `docs/development/mvp-plan.md:561` |
| 数据字段没跑过 | 「**所有数据字段都是设计出来的，没跑过一次**」 | `docs/development/mvp-plan.md:560` |

---

## 4 哪份文件过期

> 2026-11-10 注：本节行号与路径为**重构前**版本。重构后多数冲突已按 `REPOSITORY_ARCHITECTURE.md` 处置，路径已更新，行号未重算。

| 两份说法 | 过期的是 |
|---|---|
| 「the 4 competing directions」`docs/development/dashboard-plan.md:46` / 「Five competing directions」`README:80` | `docs/development/dashboard-plan.md` |
| 「**codex-cli 作为第一个实现**」`docs/development/mvp-plan.md:48` / 「已被环境证伪」`docs/development/mvp-plan.md:401` | `docs/development/mvp-plan.md` §1.2；`docs/13.1` 的 P0-1 也过期 `docs/development/mvp-plan.md:525` |
| 「You're about to write code — **start here**」`README:74` / 「执行时以 `docs/development/roadmap.md` 为准；本节保留为历史记录」`docs/development/mvp-plan.md:401` | `README` 文档地图 |
| 「All collaboration state lives under `workspace/`」`docs/foundation.md:15` / 「MVP 选择 `state.json` 作为机器权威。两者冲突」`docs/development/mvp-plan.md:55` | `docs/foundation.md`，偏离已记 OQ-18，未裁决 |
| 「Hermes Agent (the platform this project is developed on)」`directions/global-route/README.md:30` / 「`D:/github projects/` 下**不存在** Hermes 目录」`docs/architecture.md:285` | `directions/global-route` |
| 「Master Agent和Worker Agent」`相关笔记/ceaser/Diary/2026-09-25.md:18` / 「只会启用Miracle Agent」`The-Throes/2026-10-27.md:19` | 9-25 草稿 |
| 「Run a real session through the full six-step protocol」`workspace/goals.md:10` / 「其中**六步循环已过时**」`docs/decisions/register.md:364` | `workspace/goals.md` |
| 「35 cells」`workspace/state.md:24` / 「36 个格子」`docs/development/scope.md:81,150` | `workspace/state.md` |
| 「**Statuz** \| Sponge 下**信息源的子类**」`The-Throes/论文/Sponge/00_总览与论文定位.md:42` / 「**分工红线**：两者无隶属关系」`相关笔记/Sponge/03_架构与生态位.md:58` | 论文线三份 |
| 「需要Sponge做基础」`相关笔记/ceaser/Diary/2026-09-15.md:33` / 「为了让Sponge…好用，我们正在开发WAM」`相关笔记/ceaser/Diary/2026-09-16.md:22` | 相邻两天，两份都还在，没裁决 |
| 「Dashboard becomes decoration nobody uses」`docs/development/dashboard-plan.md:108` / 「Phase 1–2 **不做**：任何 Dashboard 代码」`docs/development/mvp-plan.md:298` | `docs/development/dashboard-plan.md` 的 P1 立即开工 `docs/development/dashboard-plan.md:117` |

---

## 5 待吵

1. 用户回「你看着办」，`docs/architecture.md:538` 的「在等谁：你」改不改？
2. 「✅ verified」撞上「假执行器返回成功但产物不存在」`docs/development/mvp-plan.md:272`，徽章改 ❌ 还是先挂 ⏳？
3. Unknown-unknowns 计数器显示 0 `docs/development/dashboard-plan.md:40`，`state.json` 里还躺着「how_to_answer: 问作者」`docs/specifications/execution-contract.md:196`，这条要不要也做成计数器？
4. 第二次运行「为什么」一行没变 `docs/architecture.md:539`，判据要「引用了新证据」`docs/development/mvp-plan.md:175`，这一屏照原样显示吗？
5. 72 小时没人点批准 `docs/architecture.md:519`，第一屏放「在等你」还是「这条路径已停，理由是…」`docs/architecture.md:492`？
6. 「初始回钩」`The-Throes/2026-10-19.md:17` 是不是被 6 分否掉的「提示词编写Agent」`The-Throes/2026-10-15.md:6`？下个 3 天周期打几分？
7. 白板上 Master / Worker `相关笔记/WAM/WAM Topology.canvas:11,12`，在只启用 Miracle Agent 的版本里放哪条边？
8. 1 月 1 日交付 `The-Throes/2026-10-27.md:7`，先有可跑的 Sponge 还是先有可跑的 WAM？「信息源」接口谁先冻结？
9. 「信息源」同时放 WAM 共享上下文 `The-Throes/2026-10-27.md:15` 和 Statuz `相关笔记/Sponge/03_架构与生态位.md:32`，接口契约谁写？
10. 对外那一页，WAM 挂 Lemma 的「王牌」`相关笔记/Lemma AI/Y Lemma.md:32`、Sponge 的衍生物 `相关笔记/Sponge/03_架构与生态位.md:38`，还是 CHORD 的产品 `相关笔记/CHORD/CHORD 公司简章.md:19`？
11. W1 结束没有 `.py` 文件 `docs/development/roadmap.md:142`，走固定砍单顺序 `docs/development/roadmap.md:152`，还是把它当「项目层面的结论」`docs/development/roadmap.md:142`？
12. 无单一指标的案例 #2 `docs/development/roadmap.md:64`，「做完了需外部判定」`docs/decisions/register.md:346` 由谁判？
13. 「初始回钩」「轨迹模式」「四种查看模式」`The-Throes/2026-10-15.md:9` 进不进 W4 那一次竖切 `docs/development/roadmap.md:60`？
14. 「架构不够Self-Aware」`相关笔记/WAM/WAM 的启发法设计_10_22.canvas:3` 归到「自我感知数据库」那条线，还是归到头部四问 `docs/architecture.md:538`？

---

## 6 原文在哪

`research/archive/raw-archive.md`：392 个文件全文，逐文件标 SOURCE。含 WAM Framework 工作树与 gh-pages 分支、The-Throes 全仓、git 历史里删掉的 5 篇笔记、桌面《日记(2026-10-29).md》。
