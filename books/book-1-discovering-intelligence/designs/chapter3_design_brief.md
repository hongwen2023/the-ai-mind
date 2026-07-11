# Chapter 3 Design Brief

**Working title:** 为什么抽象是人类最重要的工具之一？

**Book:** The AI Mind · Book I · Discovering Intelligence

**Author:** Codex

**Status:** Awaiting Editor-in-Chief review

**Source:** Historical Journey 03 supplies seed ideas only. The chapter will
be rewritten around the canonical Book I hidden spine and Golden Chapter
Standard.

## One Sentence

> **抽象不是把细节删掉，而是为一个目的保留足够重要的关系。**

## Knowledge Graph · Dependency Card

```text
Relationship (Chapter 1)
    ↓
Generation (Chapter 2)
    ↓
Abstraction (Chapter 3)
    ↓
Representation (Chapter 4)
    ↓
Computation and Learning (Chapters 5–6)
```

### Need Before

- Chapter 1: understanding depends on relationships, not isolated answers;
- Chapter 2: local rules, interaction, iteration, and state can generate more
  detail than a person can track directly;
- a practical distinction between a thing and the information used to reason
  about that thing.

### This Chapter

```text
complex reality
  → choose a purpose
  → preserve task-relevant relationships
  → hide replaceable detail
  → reason through a smaller interface
```

### Need After

- Chapter 4: every abstraction must be encoded in a representation;
- Chapter 5: computation transforms representations through explicit interfaces;
- Chapters 11–14: vectors, matrices, layers, and nonlinearities become reusable abstractions;
- Book III: model architectures and software systems are built from abstraction boundaries.

## Book I Question

**Book I 的问题：** 关系怎样逐步形成能够学习、推理与行动的智能系统？

**本章的问题：** 当生成过程产生的细节超过人能够逐项追踪的范围，我们怎样继续可靠推理？

**本章的回答：** 先明确任务，再把许多具体状态映射到一个更小的接口；只要接口保留了完成任务所需的差异与关系，推理就可以暂时忽略内部细节。

**下一个问题：** 被保留下来的结构怎样变成机器可以存储、比较与变换的形式？这将进入 Chapter 4 的 Representation。

## Core Question

为什么隐藏细节有时会增强理解与控制，有时却会制造危险盲区？怎样判断一个抽象究竟保留了正确结构，还是只让问题看起来更简单？

## Controlling Thesis

> **抽象是一份带目的的契约：它隐藏暂时不需要的实现细节，同时承诺保留当前任务依赖的关系。抽象的质量只能通过任务、扰动和失效边界来检验。**

这一定义避免两个极端：

- 抽象不是把内容说得更模糊；
- 抽象也不是现实本身，更不保证对所有任务都有效。

## Why This Chapter

没有抽象，Chapter 2 的复杂系统只能被逐状态、逐部件追踪。系统一旦扩大，工作记忆、代码规模和计算成本都会崩溃。

但“少看细节”本身并不可靠。忽略电路细节可以让人使用电梯；忽略制动状态却可能让驾驶界面变得危险。真正需要的不是更少信息，而是与任务匹配的信息边界。

Without abstraction, the learner or system cannot **reason across scales,
reuse a solution, or replace an implementation without rebuilding every
dependent idea**.

## Starting Mental Model

读者可能带着以下直觉进入本章：

```text
Abstraction = simplification = fewer details
```

本章要把它升级为：

```text
Abstraction
  = purpose
  + preserved distinctions
  + hidden implementation
  + explicit failure boundary
```

## Learning Objectives

完成本章后，读者能够：

1. 区分 abstraction、simplification、summary 与 representation；
2. 用 purpose、interface、invariant、hidden detail 四个问题分析一个抽象；
3. 解释为什么同一现实针对不同任务需要不同抽象；
4. 用映射与等价类表达“许多具体状态被当成同一类”；
5. 预测改变抽象边界后，哪些依赖代码或推理会失效；
6. 通过接口实现替换实验，验证软件抽象是否真的隔离实现；
7. 把抽象框架迁移到公司研究与财务模型，同时识别被隐藏的风险；
8. 说明为什么更高层抽象不一定更好，以及何时必须下钻。

## Opening Story · 急诊室里的一分钟交接

一位急诊医生接班时，不可能重新观察上一班发生的每个动作：每次测量、每句对话、每个鼠标点击和每滴输液。上一位医生只有一分钟完成交接。

如果交接只是“把内容缩短”，最短版本可以是“病人不舒服”。它几乎没有用。如果交接把所有原始记录逐字读完，新医生又无法及时行动。

真正有效的交接会围绕下一项决策组织信息：生命体征趋势、关键症状、已排除风险、当前用药、尚未解释的异常，以及什么变化需要立即升级处理。

故事建立四个问题：

- 这份交接服务什么任务？
- 哪些差异必须保留？
- 哪些实现细节可以暂时隐藏？
- 出现什么信号时，必须打开原始记录重新检查？

类比边界：医学交接涉及专业规范与生命风险；本章不教授医疗决策。它只隔离“有限接口如何支持下一步行动，以及错误抽象如何伤害行动”这一关系。

## Feynman Model · 遥控器为什么只有几个按钮？

给十二岁孩子看一台电视的遥控器。按下音量键，不需要知道红外编码、电路板、电源管理和扬声器驱动怎样协作。

遥控器提供一个小接口：

```text
intent: make sound louder
  → press volume-up
  → hidden implementation changes device state
```

好的接口让内部零件可以更换，而使用方式仍然成立。但如果遥控器只显示“工作中”，不显示静音、音量或输入源，它隐藏了完成任务所需的差异。

费曼检验不问“界面是否简单”，而问：

> 使用者需要完成哪些判断？这个界面保留了那些判断依赖的差异吗？

## First-Principles Spine

用四个位置检查抽象：

| Element | Core question | Failure when missing |
|---|---|---|
| Purpose · 目的 | 这个抽象帮助完成什么任务？ | 无法判断哪些细节重要 |
| Interface · 接口 | 使用者可以观察和操作什么？ | 内部细节继续向外泄漏 |
| Invariant · 保留关系 | 无论内部怎样变化，什么必须仍然成立？ | 替换实现后外部推理失效 |
| Hidden Detail · 隐藏细节 | 哪些差异当前可以被视为等价？ | 信息过载，无法复用或组合 |

抽象不是单向删减。它建立一条契约：内部可以变化，外部依赖的关系必须保持。Failure Modes 将持续追问这份契约何时不再成立。

## Mathematics Spine · 从具体状态到等价类

数学采用“现实对象 → 分组图示 → 映射 → 任务保持”四层递进。

设具体状态属于集合 (X)。抽象映射把它变成较小空间里的描述：

\[
A:X\rightarrow Z
\]

如果两个具体状态在当前任务下被视为同一类，可以写成：

\[
x_1 \sim_A x_2
\quad\text{when}\quad
A(x_1)=A(x_2)
\]

但“映射到同一类”只有在任务上才有意义。若真实任务由 (g(x)) 表示，希望存在一个较简单的决策 (h)，使：

\[
g(x)\approx h(A(x))
\]

直觉解释：如果只看抽象 (A(x))，仍能完成原任务，抽象保留了有用结构；如果不同答案所需的状态被压进同一类，抽象就过度丢失信息。

本章不教授信息论、充分统计量、范畴论或形式化验证。数学只让“任务相关的保真”可以被检查。

## Planned Visualization

### Figure 1 · One Reality, Different Abstractions

同一城市分别抽象成地铁图、海拔图和行政区图。三张图都隐藏大量细节，但保留的关系不同。图示回答：为什么抽象没有脱离任务的统一优劣排序？

### Figure 2 · Abstraction Contract

```text
caller
  → interface
  → hidden implementation A / hidden implementation B

invariant remains stable
```

图示回答：为什么替换内部实现可以检验接口是否真正隔离细节？

## Engineering Spine · 接口、替换与泄漏

正文先使用普通 Python 函数，而不是直接进入 class hierarchy 或神经网络框架。

计划接口：

```python
def score_company(data_source) -> float:
    ...
```

两个内部实现分别读取字典与对象，但对调用者维持同一契约。Perturbation Test 要求读者：

1. 替换内部实现，观察调用者是否无需修改；
2. 改变返回单位，观察隐含契约如何破裂；
3. 删除异常状态，观察“简单接口”如何隐藏失败；
4. 让调用者读取内部字段，观察 abstraction leakage 怎样产生耦合。

迁移到 AI 时，只预览 Tensor、Layer 与 Model API 作为抽象边界。正式实现留给后续章节。

## AI × Finance · Driver Model 是抽象，不是公司本身

投资者不可能把公司所有合同、员工决策、客户行为和会计记录同时装进模型。研究通常构建 Driver Tree：

```text
revenue
  = users
  × usage
  × monetization
```

这份抽象保留增长驱动关系，隐藏大量运营细节。它对情景分析可能有效，却可能漏掉收入确认、渠道库存、客户集中度、监管约束或网络效应变化。

学习任务要求读者为同一家公司建立两种抽象：

- 预测下一季度利润的 operating model；
- 判断五年竞争优势的 strategic model。

然后解释为什么两者不能互换。金融部分的核心不是“模型越简单越好”，而是：抽象必须与决策期限、风险和可验证证据匹配。

## Research Corner · 模型学到的是哪一种抽象？

研究问题：神经网络的中间表示何时对应可复用的抽象，何时只是对训练分布有效的压缩捷径？

正文只建立三类证据：

1. **Transfer:** 表示能否支持新任务或新分布？
2. **Intervention:** 改变某个内部方向是否稳定改变目标行为？
3. **Boundary:** 在哪些反例上，表面相同的抽象会分裂？

Research Corner 不提前教授 representation learning 或 mechanistic interpretability。它只让读者看到：命名一个隐藏单元“概念”不是证据；抽象需要通过迁移、干预和边界测试。

候选阅读路标将在正文创作前核验原始来源，并限制在 2–3 项。

## Common Illusions

- “内容更短”不等于“抽象更好”；
- “名字更专业”不等于“关系更清楚”；
- “接口能运行”不等于“契约完整”；
- “高层模型更优雅”不等于“底层细节不重要”；
- “一个表示与概念相关”不等于“系统使用了那个概念”；
- “财务模型解释历史”不等于“它保留了未来会变化的驱动”。

每项错觉都要配一个更强测试：换任务、换实现、制造边界案例或主动下钻。

## Failure Modes

### Wrong Purpose

抽象为一个任务设计，却被迁移到另一个任务；地铁图不能回答洪水风险。

### Lost Distinction

两个对决策不同的状态被压入同一类别，导致无法恢复关键差异。

### Leaky Abstraction

调用者必须知道内部实现才能正确使用接口，替换实现会造成连锁修改。

### Frozen Abstraction

现实关系改变后，旧分类仍被当作自然事实；金融行业分类与模型标签尤其容易发生这种问题。

### Abstraction as Authority

模型输出因为简洁而显得客观，但隐藏了假设、缺失变量和测量误差。

## Mental Model Upgrade

### Before

```text
Abstraction
  = fewer details
  = easier explanation
```

### After

```text
Abstraction
  = task-specific contract
  = preserved relationships
  + hidden implementation
  + known boundary
```

升级完成的证据不是能复述定义，而是能说明：一个抽象为谁服务、保留什么、隐藏什么，以及哪种扰动会使它失效。

## Learning Package Plan

### Notebook · Abstraction Boundary Lab

使用一个小型数据处理任务比较三种接口：原始记录、手工特征和任务专用摘要。每轮实验必须先预测：改变任务后，哪一种抽象会丢失必要信息？

### Understanding Audit

- **Explain:** 为什么抽象不是单纯删掉细节？
- **Predict:** 改变任务或接口契约后，哪个依赖会先失效？
- **Reconstruct:** 从空白页重建 Purpose / Interface / Invariant / Hidden Detail 四要素与映射关系；
- **Transfer:** 为一个新的工程或金融问题设计抽象，并列出必须下钻的触发条件。

### Capability Milestone

After completing the Learning Package, the learner can:

- **Explain:** distinguish abstraction from vague simplification;
- **Predict:** identify which task change will break an abstraction;
- **Build:** define and test a small interface with replaceable implementations;
- **Read:** inspect a model or research claim for hidden assumptions and lost distinctions.

## Exercise Evidence

练习按证据递进：识别现实中的接口、比较同一对象的多个抽象、手算映射与等价类、替换 Python 实现、诊断 abstraction leakage、重构 Driver Tree，并设计一个能暴露错误抽象的反例。

## Connection and Bridge

Chapter 2 展示简单规则如何生成超出逐项追踪能力的复杂结果。Chapter 3 提供继续推理的办法：按任务建立边界，把可替换的细节藏在接口后，同时保留必要关系。

但抽象仍然只是一个关系选择。机器无法直接计算“重要关系”这句话。它需要数字、符号、类别、向量或其他具体形式。

> **如果抽象决定保留什么，那么机器究竟用什么形式把它保留下来？**

这进入 Chapter 4：**为什么世界需要表示（Representation）？**

## Scope Boundaries

本章不完整教授：

- 信息论与最小描述长度；
- 充分统计量；
- 范畴论或抽象代数；
- 面向对象设计模式大全；
- representation learning；
- mechanistic interpretability；
- 形式化验证。

这些主题只在服务“任务相关的保真边界”时准确预览。

## Definition of Done

- [ ] Opening Story 让抽象成为行动所必需，而不只是知识分类；
- [ ] Purpose / Interface / Invariant / Hidden Detail 贯穿正文与练习；
- [ ] 数学映射中的每个符号都有任务直觉；
- [ ] 工程实验通过替换实现和破坏契约来检验抽象；
- [ ] AI × Finance 比较至少两个不可互换的公司抽象；
- [ ] Research Corner 区分相关、可迁移与可干预证据；
- [ ] Common Illusions 均配有更强测试；
- [ ] Mental Model Upgrade 描述可验证的认知变化；
- [ ] Bridge 使 Representation 成为下一个必要问题。

## Questions for Editorial Review

1. 急诊交接是否足够具体，同时避免把医学实践过度简化？
2. “任务相关的契约”是否适合作为 abstraction 的统一定义？
3. Purpose / Interface / Invariant / Hidden Detail 是否能贯穿数学、工程与金融迁移？
4. 映射与等价类是否处于 Book I Chapter 3 合适的数学深度？
5. 工程实验是否真正检验抽象边界，而不只是演示函数调用？
6. Research Corner 是否准确提出问题，又没有预支 Chapter 4 与后续研究内容？
