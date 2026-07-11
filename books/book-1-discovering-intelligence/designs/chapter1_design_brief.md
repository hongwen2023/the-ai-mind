# Chapter 1 Design Brief

**Working title:** 为什么理解比记忆重要？

**Book:** The AI Mind · Book I · Discovering Intelligence

**Author:** Codex

**Status:** Draft v0.1 · Awaiting Editorial Review

**Source:** Historical Journey 01 provides ideas only; structure and prose will be rewritten.

## Core Question

为什么“我记得答案”和“我理解问题”不是同一件事？什么证据足以说明一个 AI 概念已经真正属于学习者？

## Controlling Thesis

> **记忆保存见过的答案；理解建立答案之间的关系，使人能够解释、预测、重建并迁移。**

本章不会贬低记忆。事实、符号与经验是理解的材料；问题在于把记得多误认为理解深。

## Why This Chapter

Prelude 给了读者第一张 AI 地图，但看过地图、记住路线和理解道路如何连接仍是三种能力。如果不先区分熟悉感与理解，后续学习会反复出现同一种错觉：视频听懂却写不出，公式眼熟却不能推导，Notebook 能运行却不能调试，投资观点记得牢却不能应对驱动变化。

Chapter 1 将建立全书通用的“理解验收标准”。

## Learning Objectives

读者完成本章后能够：

1. 区分 Familiarity、Recall、Understanding 与 Transfer；
2. 用“解释、预测、重建、迁移”四项测试检查理解；
3. 说明记忆为何必要但不充分；
4. 从少量样本提出规则，并用新样本和反例检验；
5. 对 AI 代码执行 perturbation test，而不是只确认它能运行；
6. 把理解测试迁移到投资研究；
7. 区分模型“理解”的行为证据、因果证据与机制证据。

## Opening Story · 地铁停运之后

故事承接 Prelude，但正文可独立阅读。

两位旅行者都记住了从酒店到目的地的路线。第二天，一条地铁线临时停运。第一位记住的是固定换乘步骤，路线改变后只剩失效答案；第二位理解线路关系，能根据地图重新规划。

转入 AI：记住训练脚本等于记住路线；理解数据、模型、Loss、Gradient 与 Update 的关系，才允许学习者在形状变化、API 改动或训练异常时重新规划。

故事的作用是用“条件变化”让记忆与理解的差异可见。

## Feynman Model · 答案卡与小机器

- 记忆像答案卡：相同问题出现时能快速取回答案；
- 理解像透明小机器：条件改变后，仍能根据内部关系产生答案。

答案卡并非无用，小机器也需要事实作为零件。类比边界：人的理解不是机械装置；“小机器”只表示一个能产生预测并接受反例的关系模型。

## First Principles

1. 学习者只能接触有限经验，逐条记忆无法覆盖未来情况。
2. 应对变化需要保留观察之间的关系。
3. 关系模型必须产生可检验后果，否则“理解”只是主观确信。
4. 有限观察可能支持多种规则，因此理解必须保持可修正。

本章用四项互补证据检验理解：

| Test | 核心问题 | AI 学习证据 |
|---|---|---|
| Explain | 为什么得到这个结果？ | 能连接数据、模型、Loss 与更新 |
| Predict | 条件改变会怎样？ | 能预判学习率、维度或数据变化的后果 |
| Reconstruct | 忘记细节后能恢复吗？ | 能从原则重建最小流程 |
| Transfer | 新场景仍能使用吗？ | 能迁移到新模型、系统或金融问题 |

## Mathematics Spine

给出三个观察：`(1,3), (2,5), (3,7)`。

记忆策略保存三对答案；理解策略提出：

\[
y = 2x + 1
\]

它压缩样本、预测 `x=4` 时 `y=9`，也能被新样本证伪。

关键反转：有限点可以被多条曲线完美拟合。选择简单规则包含归纳假设。因此，理解不是找到唯一真理，而是提出目前最简洁、可检验、愿意被修正的模型。

本章只建立直觉，不正式讲多项式插值、Occam's Razor 或 Inductive Bias。

## Engineering Spine

给出最小训练循环：

```python
prediction = model(x)
loss = loss_fn(prediction, target)
optimizer.zero_grad()
loss.backward()
optimizer.step()
```

读者执行 perturbation test：删除 `zero_grad()`、交换 `backward()` 与 `step()`、改变目标形状，并在运行前预测后果。验收重点不是记住 API，而是能从“预测—比较—求责—更新”重建逻辑。

计划配套一个短实验，对比 lookup table 与规则函数在已见和未见输入上的行为，并用反例迫使读者更新模型。

## AI × Finance

案例：某公司毛利率连续三个季度上升。

记忆型结论是“毛利率改善，所以值得买入”；理解型研究要建立产品结构、定价、成本、利用率与一次性因素构成的 driver tree，并通过四项测试：

- Explain：哪个驱动解释历史？
- Predict：关键变量变化时结果如何变化？
- Reconstruct：不看研报能否重建逻辑？
- Transfer：框架能否用于同行？

必须强调：金融机制会受竞争、管理行为和市场反身性影响。理解是可证伪、可更新的因果假设，不是永久正确的故事。

## Research Corner

核心问题：

> 模型在新任务上答对时，什么证据能区分可迁移结构与训练模式复用？

只介绍三个证据层次：

1. Behavioral：在未见组合、反事实与分布变化下是否稳定？
2. Causal：干预输入或内部表征时，行为是否按假设改变？
3. Mechanistic：能否找到执行能力的内部特征或回路？

候选阅读方向限于 memorization versus generalization、grokking 和 mechanistic interpretability。本章不裁决 LLM 是否具有意识。

## Figures and Learning Artifacts

计划两张 SVG：

1. `Four Tests of Understanding`：四项互补证据，不画成能力阶梯；
2. `Lookup Table vs Generative Rule`：两者在已见输入上都正确，但对未见输入行为不同。

计划工件：`labs/book1/chapter01-understanding-audit.md`，用于四项测试、扰动测试、一周后重建和反例更新记录。

## Failure Modes

- 把记忆写成理解的敌人；
- 把流畅解释当作充分证据；
- 把简洁规则当作最终真理；
- 把人类理解直接投射到模型；
- 追求“完全理解”而迟迟不进入实现。

## Exercise Evidence

练习依次要求读者：区分熟悉与理解、执行四项审计、用反例更新规则、扰动训练循环、把投资观点改写为 driver tree 与反证条件，并设计区分模式复用与结构迁移的实验。

Teach Back 面向十二岁孩子、工程师和投资者，分别使用答案卡、调试和 driver tree 语言。

## Connection and Bridge

与 Prelude 的连接：

> 记住地图，是否等于理解地图？

地铁停运把静态地图变成必须应对变化的模型。

通往 Chapter 2：Chapter 1 表明理解常用较少规则组织较多观察，于是自然出现下一个问题：

> 少量简单规则怎样组合出复杂行为？

## Scope Boundaries

本章不完整教授认知神经科学、统计学习理论、多项式插值、正式泛化界、意识哲学或 mechanistic interpretability 方法。这些内容只在服务核心问题时预览。

## Definition of Done

- [ ] 开篇可独立阅读并自然承接 Prelude；
- [ ] 明确说明记忆必要但不充分；
- [ ] 四项测试贯穿数学、工程、金融与练习；
- [ ] 数学例子同时展示规则压缩与有限样本歧义；
- [ ] Research Corner 区分行为、因果和机制证据；
- [ ] 每个 Learning Objective 都有对应练习；
- [ ] Bridge 使 Chapter 2 成为必要下一步。

## Questions for Editorial Review

1. 地铁停运作为 Prelude 续篇，是否连续且可独立阅读？
2. 四项测试是否适合作为全书通用验收标准？
3. 数学锚点是否适合 Chapter 1 难度？
4. 工程与金融迁移是否足够具体？
5. Research Corner 是否准确且未过度预支后续内容？
