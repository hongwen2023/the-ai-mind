# Chapter 2 Design Brief

**Working title:** 为什么复杂系统可以来自简单规则？

**Book:** The AI Mind · Book I · Discovering Intelligence

**Author:** Codex

**Status:** Draft v0.1 · Awaiting Editorial Review

**Source:** Historical Journey 02 provides the seed idea only; claims,
structure, examples, and prose will be rewritten.

## Dependency Card

### Need Before

- Prelude: knowledge is a map of relationships, not a list of names;
- Chapter 1: understanding uses relationships to explain, predict,
  reconstruct, and transfer;
- minimal notation: a state can change from one step to the next.

### This Chapter

```text
Local Rule + Iteration + Interaction + State
  ↓
Global Pattern and Dynamic Behavior
```

### Need After

- Chapter 3: abstraction hides detail while preserving usable structure;
- Chapter 4: representation decides which state and relationships are visible;
- Chapters 13-14: simple neural transformations compose into richer behavior;
- Part III: scaling and modern AI revisit emergence with stronger evidence.

## Core Question

为什么没有中央设计者、没有一条“复杂指令”，简单局部规则仍可能形成全局结构、动态模式和难以预测的行为？

## Controlling Thesis

> **复杂行为不一定需要复杂规则；当简单关系被反复执行、彼此交互并保留状态时，全局结构可能从局部过程里生长出来。**

本章使用“可能”而不是“必然”。简单规则也可能产生平凡、脆弱或无用的结果；复杂行为也不证明系统拥有理解或智能。

## Why This Chapter

Chapter 1 把理解定义为建立关系，并用较少规则组织多个观察。现在出现自然问题：少量关系的表达能力为什么可以如此强？

如果读者只看到 Transformer、市场或分布式系统的最终规模，就会把复杂性误认为来自某个同样复杂的中央公式。本章要建立一种生成视角：先找局部更新，再追踪重复、交互和历史怎样放大全局后果。

这为后续抽象、表示、神经网络、训练循环与 Agent 系统提供共同语言。

## Learning Objectives

读者完成本章后能够：

1. 区分 simple rule、simple behavior 与 predictable behavior；
2. 用 Local Rule、Iteration、Interaction、State 四个要素分析复杂系统；
3. 从局部更新式解释全局模式如何逐步生成；
4. 预测初始状态、更新顺序或规则改变可能带来的影响；
5. 解释为什么神经网络的复杂表示可以来自简单层的组合；
6. 把反馈回路分析迁移到市场和公司系统；
7. 区分真正的能力跃迁与评价指标造成的“突然涌现”；
8. 说明何时“寻找简单规则”会成为过度简化。

## Opening Story · 没有指挥的人浪

一座体育场里，人浪绕看台前进。没有人掌握全场时间表，也没有中央指挥逐排发令。每位观众只做很少的事：观察邻近区域，在浪到来时站起，再坐下。

局部动作很简单，全局图案却会移动、加速、衰减，甚至在不同区域分裂。人数、延迟、注意力和看台结构稍有变化，人浪可能顺利传播，也可能几秒后消失。

故事要引出四个问题：

- 每个人遵循什么局部规则？
- 为什么一次动作必须不断重复？
- 邻居之间如何相互影响？
- 当前状态怎样影响下一时刻？

这四个问题比“谁设计了人浪”更接近复杂系统的生成机制。

## Feynman Model · 方格世界

给十二岁孩子一排只有黑白两色的方格。每个方格下一轮变成什么颜色，只看自己附近三个方格。所有方格同时更新，再重复很多轮。

没有任何方格知道最终图案，也没有一条规则直接画出整幅图。图案是更新过程留下的历史。

类比边界必须明确：真实神经网络、市场和社会系统不只是黑白方格；它们的规则会学习，参与者会反应，更新也未必同步。方格世界只用来隔离“局部规则怎样生成全局模式”这一件事。

## First-Principles Spine

复杂行为出现至少需要观察四个位置：

| Element | 核心问题 | 缺失时可能怎样 |
|---|---|---|
| Local Rule · 局部规则 | 一个部分如何根据附近信息更新？ | 没有可重复的生成机制 |
| Iteration · 迭代 | 同一更新如何跨时间重复？ | 只得到一次静态变换 |
| Interaction · 交互 | 一个部分的状态怎样影响其他部分？ | 各部分彼此独立，难形成整体结构 |
| State · 状态 | 过去留下什么信息影响下一步？ | 系统缺少路径与历史依赖 |

本章将 Emergence 操作性定义为：全局可观察结构由局部交互生成，而该结构没有被直接写进单个局部规则。它不意味着超自然、不可研究或一定不可预测。

## Mathematics Spine · 一个更新式如何展开成历史？

用状态更新建立最小数学语言：

\[
\mathbf{s}_{t+1}=F(\mathbf{s}_t)
\]

它只表示：下一时刻的整体状态，由当前状态经过更新规则产生。

随后把整体拆成局部：

\[
s_i^{(t+1)}=f\left(s_{i-1}^{(t)},s_i^{(t)},s_{i+1}^{(t)}\right)
\]

每个方格只读取附近状态，却共同形成下一行全局图案。

核心实例使用 elementary cellular automaton。计划选择一个规则清晰、图案具有层次的版本，并让读者比较：

- 相同规则，不同初始状态；
- 相同初始状态，修改一位规则；
- 同步更新与顺序更新。

数学目的不是教授元胞自动机分类，而是让“规则 + 状态 + 重复 = 动态系统”可计算。

## Engineering Spine

工程迁移聚焦两个层次，不展开完整深度学习理论。

### Layer Composition

单层神经网络通常只执行结构明确的变换：

\[
\mathbf{h}_{k+1}=\phi(W_k\mathbf{h}_k+\mathbf{b}_k)
\]

复杂表示不是写在某一层里，而是在许多简单变换组合后形成。这里仅预览，正式数学留给 Chapters 13-14。

### Training Iteration

预测、损失、梯度和更新组成短循环；重复许多次后，参数与行为发生巨大变化。本章只分析“重复反馈如何积累”，不提前教授 Backpropagation。

Perturbation tests 将要求读者先预测：减少层数、去掉交互、冻结状态或改变更新顺序，会破坏哪种能力。

## AI × Finance · 市场不是一条公式

金融映射不把价格归结为几条永恒规律，而分析参与者、约束和反馈怎样共同生成市场行为。

核心案例使用一个简化反馈环：

```text
盈利预期上调
  ↓
买盘与价格上升
  ↓
趋势资金 / 风险预算变化
  ↓
更多买盘或仓位约束
  ↓
估值、融资与公司行为改变
  ↺
新的基本面与预期
```

读者需要区分：

- local rule：单个参与者按什么约束行动；
- interaction：订单与价格如何传递影响；
- state：仓位、流动性和历史价格留下什么路径依赖；
- feedback：正反馈何时放大，负反馈何时稳定。

边界：市场规则会被参与者学习和改变，不能把一个漂亮反馈图当成稳定真理。

## Research Corner · 涌现是真跳变，还是测量方式？

研究问题：大型模型的某些能力看似在规模增加后突然出现，这种“涌现”来自内部机制转变，还是评价指标把连续改善显示成离散跳跃？

正文阶段只保留两类证据：

1. Scaling observation：能力指标随模型规模怎样变化；
2. Measurement intervention：改变指标、提示或任务分解后，跳变是否仍存在。

候选阅读路标：Wei et al. 的 emergent abilities 观察，以及 Schaeffer et al. 对非线性或离散指标造成涌现假象的分析。正式写作前核验原始论文。

本章不解决 scaling laws，也不把“涌现”当作智能证明。

## Common Illusions

- “规则简单”不等于“结果简单”；
- “规则确定”不等于“长期容易预测”；
- “出现全局图案”不等于“存在中央设计者”；
- “行为突然出现”不等于“内部机制突然形成”；
- “能模拟图案”不等于“解释了真实系统”。

## Figures and Learning Package

计划两张 SVG：

1. `Local Rules to Global Pattern`：四要素如何连接局部与全局；
2. `Cellular Automaton Evolution`：一个初始状态经过重复局部更新形成多行图案。

计划 Notebook：实现一维元胞自动机，修改初始状态、局部规则和更新方式；每次运行前必须写预测。

计划 Understanding Audit：

- Explain：为什么全局图案没有被直接写入局部规则？
- Predict：改变初始状态或交互范围会怎样？
- Reconstruct：从空白页重建四要素与状态更新式；
- Transfer：把框架迁移到神经网络训练或市场反馈。

Learning Package 将统一索引 Chapter、Notebook、Audit、Figures 和 Glossary。

### Capability Milestone

After completing the Learning Package, the learner can:

- **Explain:** identify how local rules, iteration, interaction, and state
  generate a global pattern;
- **Predict:** state how a rule, initial condition, or update-order change may
  alter system behavior before running it;
- **Build:** implement and perturb a one-dimensional cellular automaton;
- **Read:** evaluate a basic emergence claim by separating behavior change
  from measurement effects.

## Exercise Evidence

练习依次要求读者：识别四要素、手算三轮方格更新、运行前预测代码扰动、拆解一个 AI 系统的组合关系、画出金融反馈回路，并设计区分“真实能力跃迁”和“指标跳变”的实验。

## Connection and Bridge

与 Chapter 1 的连接：理解依赖关系；Chapter 2 研究少量关系如何在重复和交互中生成复杂结果。

通往 Chapter 3：当规则、状态和层级不断增加，人已经无法同时追踪所有细节。于是出现下一个必要工具：

> 我们怎样隐藏暂时不重要的细节，只保留可以继续推理的结构？

这进入 Chapter 3：**为什么抽象是人类最重要的工具之一？**

## Scope Boundaries

本章不完整教授：

- 计算复杂性理论；
- 混沌理论与 Lyapunov 指数；
- 元胞自动机分类史；
- Scaling Laws；
- 深度网络表达能力定理；
- 市场微观结构模型；
- 多智能体系统。

这些内容只在服务“简单局部关系如何生成复杂全局行为”时预览。

## Definition of Done

- [ ] 一个 controlling idea 贯穿方格、AI 与金融案例；
- [ ] 明确说明简单规则不保证复杂、有用或可预测行为；
- [ ] 四要素贯穿数学、Notebook、练习与 Audit；
- [ ] 数学更新式中的每个符号都有直觉解释；
- [ ] Notebook 每个实验要求先预测后运行；
- [ ] Research Corner 区分能力变化与测量方式；
- [ ] Common Illusions 为每个弱判断提供更强测试；
- [ ] Bridge 使抽象成为 Chapter 3 的必要工具；
- [ ] Learning Package 各工件职责明确。

## Questions for Editorial Review

1. 体育场人浪是否足够直观，又不会把复杂系统简化成同步模仿？
2. Local Rule、Iteration、Interaction、State 是否适合作为全章统一框架？
3. 元胞自动机是否是合适的数学与 Notebook 锚点？
4. 神经网络与市场迁移是否保持正确边界，未过度类比？
5. Emergence 的研究问题是否准确且没有预支 Scaling Laws 章节？
