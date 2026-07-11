# Chapter 4 Design Brief

**Working title:** 为什么世界需要表示（Representation）？

**Book:** The AI Mind · Book I · Discovering Intelligence

**Author:** Codex

**Status:** Awaiting Editor-in-Chief review

**Source:** Historical Journey 04 supplies seed ideas only. The chapter will
be rewritten around the canonical Book I hidden spine and Golden Chapter
Standard.

## One Sentence

> **表示不是现实的副本，而是让某些关系变得可计算、同时让另一些关系变得不可见的选择。**

## Knowledge Graph · Dependency Card

```text
Relationship (Chapter 1)
    ↓
Generation (Chapter 2)
    ↓
Abstraction as Contract (Chapter 3)
    ↓
Representation as Computable Form (Chapter 4)
    ↓
Computation (Chapter 5)
    ↓
Learning (Chapter 6)
```

### Need Before

- Chapter 1: understanding depends on reusable relationships;
- Chapter 2: local state and interaction can generate global behavior;
- Chapter 3: abstraction chooses which task-relevant relationships to
  preserve and which implementation details to hide.

### This Chapter

```text
world
  → observation
  → encoding choice
  → representation
  → available operations and comparisons
  → model-visible world
```

### Need After

- Chapter 5: computation transforms representations, not reality directly;
- Chapter 6: learning changes parameters to discover useful relationships in a representation;
- Chapters 11–12: vectors and matrices make representation geometry explicit;
- Part III: Embedding, hidden state, attention, and learned representation;
- Book III: Tokenizer and architecture choices define what an LLM can process efficiently.

## Book I Question

**Book I 的问题：** 关系怎样逐步形成能够学习、推理与行动的智能系统？

**本章的问题：** 抽象决定保留什么以后，机器用什么形式保存这些关系，并据此区分、比较与变换世界？

**本章的回答：** 通过表示映射，把观察转换为可计算状态；映射不仅编码信息，也决定哪些对象显得相近、哪些差异被保留，以及哪些操作变得容易。

**下一个问题：** 一旦关系被写成可操作形式，有限的机械步骤怎样把输入表示变成新的表示与结果？这进入 Chapter 5 的 Computation。

## Core Question

为什么同一现实换一种表示后，会让同一个问题突然变得容易、困难，甚至无法回答？怎样判断表示保留的是任务结构，还是训练数据中的偶然捷径？

## Controlling Thesis

> **表示是一种有后果的编码选择：它把观察映射到可计算空间，并由此定义系统能够看见的差异、邻近关系与可用操作。模型只能从表示允许它区分的世界中学习。**

本章持续区分：

- Reality：独立于模型而存在或发生的对象与过程；
- Observation：传感器、文本、表格或制度记录捕获到的部分；
- Representation：系统实际接收并操作的编码结构；
- Model：在该结构上执行比较、变换与预测的函数。

## Why This Chapter

Chapter 3 说明抽象是带目的的 Contract，却留下一个工程缺口：机器不能直接操作“增长”“风险”“猫”或“含义”。这些词必须变成位、数字、类别、像素、Token、向量或图结构。

不同形式不是同义包装。把星期编码成 `0,1,...,6`，会让星期日与星期一看起来相距 6；把它编码在圆上，这两个日期重新成为邻居。表示改变，几何与可学习关系也改变。

Without representation, a system cannot **store distinctions, compare
states, apply computation, or receive a learnable signal**.

## Starting Mental Model

读者可能带着以下直觉进入本章：

```text
Representation
  = convert reality into numbers
```

本章要把它升级为：

```text
Representation
  = observation boundary
  + encoding
  + geometry
  + available operations
  + lost distinctions
```

## Learning Objectives

完成本章后，读者能够：

1. 区分 Reality、Observation、Representation 与 Model；
2. 解释为什么数据不是现实，也不自动是适合任务的表示；
3. 用 Encoding、Distinction、Geometry、Operation、Decoder 五个位置检查表示；
4. 比较 categorical、ordinal、one-hot 与 cyclical encoding 的结构后果；
5. 用映射 (R:O\rightarrow Z) 表达观察到表示的转换；
6. 预测 representation collision 和错误几何如何限制模型；
7. 实现并扰动一个小型编码实验，而不是直接调用 Embedding API；
8. 迁移到金融数据，识别会计口径、频率、缺失值与时间边界造成的表示风险；
9. 说明为什么“可预测”不等于表示捕获了人类期望的因果因素。

## Opening Story · 火星探测器看到的不是火星

一台探测器落在火星表面。它周围有岩石、尘埃、温度变化、辐射和风。地球上的研究团队却没有直接接触火星。

他们收到的是遥测包：传感器读数、时间戳、压缩图像、位置坐标、状态码和缺失标记。

探测器眼前的世界与科学家屏幕上的世界之间，至少经过：

```text
physical world
  → sensor
  → sampling
  → quantization
  → compression
  → transmission
  → decoded representation
```

如果温度分辨率太粗，短暂峰值会消失；如果图像压缩丢掉细纹，岩层结构可能不可恢复；如果时间戳错位，原本相关的事件会被当成无关。

科学家不是在“看火星本身”，而是在根据一套表示推理火星。表示不是无害容器，它决定哪些证据能够抵达模型。

故事建立五个问题：

- 世界的哪一部分被观察？
- 观察怎样被编码？
- 哪些差异在编码后仍可区分？
- 编码空间里的“接近”代表什么？
- 哪些问题已经因为表示选择而无法回答？

类比边界：科学仪器经过严格校准，机器学习数据集可能来自更复杂的社会流程。火星遥测用于隔离“模型只接触表示”这一事实，不代表所有表示都由单一传感器产生。

## Feynman Model · 同一个星期，三种摆法

给十二岁孩子七张卡片，写着 Monday 到 Sunday。

第一种摆法按编号排成直线：

```text
Mon Tue Wed Thu Fri Sat Sun
 0   1   2   3   4   5   6
```

它保留顺序，却让 Sunday 与 Monday 看起来最远。

第二种摆法把每一天放进一个独立盒子。它避免“Friday 比 Tuesday 大”这种误解，却让所有不同日期看起来同样不相似。

第三种摆法围成圆：

```text
        Mon
   Sun       Tue
  Sat         Wed
      Fri Thu
```

圆形保留周期邻近，却不方便直接表达“第几个工作日”。

没有一种编码脱离任务永远最好。表示像摆放卡片的方式：对象没变，系统可直接利用的关系变了。

## First-Principles Spine

用五个位置审计表示：

| Element | Core question | Failure when missing |
|---|---|---|
| Observation · 观察 | 世界的哪部分进入系统？ | 把未观测事实误当成模型已知 |
| Encoding · 编码 | 状态怎样写成符号或数字？ | 语义、单位与缺失规则含混 |
| Distinction · 区分 | 哪些不同状态仍能被分开？ | Representation collision |
| Geometry · 几何 | 距离、方向和邻近代表什么？ | 模型学习错误相似性 |
| Operation · 操作 | 哪些比较与变换在该形式上自然？ | 任务需要的关系难以计算 |

Decoder 作为检查工具贯穿：给定表示，能恢复什么、不能恢复什么？本章不要求所有表示可逆；不可逆本身就是必须声明的边界。

## Mathematics Spine · 从观察到可计算空间

数学采用“同一对象的多种编码 → 坐标图 → 距离比较 → 映射与碰撞”递进。

设可获得的观察属于集合 (O)，表示空间为 (Z)，编码映射为：

\[
R:O\rightarrow Z
\]

模型不直接接收 (o)，而接收：

\[
z=R(o)
\]

然后执行：

\[
\hat{y}=f(z)=f(R(o))
\]

这个分解使错误来源可见：预测失败可能来自模型 (f)，也可能在表示 (R) 处已经丢失必要差异。

### Representation Collision

若两个任务相关状态被编码为同一表示：

\[
o_1\neq o_2,
\qquad
R(o_1)=R(o_2)
\]

任何只看 (z) 的下游模型都无法再区分它们。更多参数不能恢复从未进入表示的信息。

### Geometry

若表示是向量，可计算距离：

\[
d(z_i,z_j)
\]

但距离只有在编码赋予它意义时才有解释。邮政编码 `10001` 与 `10002` 数值接近，不自动表示地理或经济相似；类别 ID 的减法通常没有任务含义。

周期日期计划使用：

\[
R(d)=\left(
\cos\frac{2\pi d}{7},
\sin\frac{2\pi d}{7}
\right)
\]

其目的不是提前教授三角函数，而是展示：改变表示空间，可以让周期邻近成为几何邻近。

## Planned Visualizations

### Figure 1 · World to Model-Visible World

展示 Reality → Observation → Encoding → Representation → Model，并在每个边界标出一种损失：未观测、采样、压缩、碰撞。

### Figure 2 · Three Geometries of a Week

比较 ordinal line、one-hot simplex 与 cyclical circle。图示回答：同一语义如何因编码而产生不同距离？

## Engineering Spine · 先设计结构，再选择 API

Notebook 使用星期需求预测的最小实验，比较：

1. ordinal encoding：单个整数；
2. one-hot encoding：七个独立位置；
3. cyclical encoding：二维圆坐标。

Perturbation Tests 要求先预测：

- Sunday 与 Monday 的距离在哪种表示中最小？
- 打乱类别 ID 后，哪些模型输出不应改变？
- 把 missing value 编码为 `0` 会与哪个真实状态碰撞？
- 新类别出现时，固定 one-hot interface 怎样失效？

工程重点不是比较模型排行榜，而是建立 representation test：

```text
semantic claim
  → encode examples
  → inspect geometry
  → perturb labels or units
  → test downstream invariance
```

Embedding 只作为未来预览：它让表示可以从训练反馈中学习，但“可学习”不自动等于“学到正确结构”。

## AI × Finance · 公司向量怎样制造“可比公司”？

市场里的公司没有天然坐标。分析者选择：

```text
[growth, gross margin, capital intensity, leverage, valuation]
```

就把公司映射到一个特征空间。距离近的公司会被视为可比，但该结论完全依赖：

- 指标定义；
- 时间窗口；
- 单位和标准化；
- 缺失值处理；
- 会计口径；
- 是否包含商业模式与制度差异。

核心实验比较同一组公司在三种表示下的邻居：

1. raw scale：市值和收入主导距离；
2. standardized ratios：增长和利润率获得更大权重；
3. task-specific representation：为估值或风险分别选择特征。

读者必须解释：表示没有“发现”可比公司，它先定义了什么叫可比。

边界案例包括 point-in-time 数据、survivorship bias、restatement 与 look-ahead leakage。它们说明错误常发生在模型之前：现实被记录成什么样，决定模型有机会学到什么。

## Research Corner · 好表示能否从数据中自动出现？

研究问题：只给系统大量观察，是否足以恢复世界中人类关心的生成因素？

[Bengio, Courville, and Vincent (2013)](https://arxiv.org/abs/1206.5538) 系统讨论了表示如何让不同解释因素更容易被下游任务利用，并把 representation learning 作为深度学习的重要目标。

但“数据里存在因素”不代表无监督算法能唯一恢复人类期望的分解。[Locatello et al. (2019)](https://proceedings.mlr.press/v97/locatello19a.html) 证明，在没有模型与数据归纳偏置时，完全无监督的 disentanglement 不可识别，并用大规模实验挑战了若干常见假设。

本章不教授 VAE 或 disentanglement 指标，只建立研究纪律：

```text
learned representation
  ≠ neutral discovery of reality

data + objective + architecture + supervision
  → one selected representation
```

Evidence Standard 延续 Chapter 3：

- **Transfer:** 新任务或新分布仍有用吗？
- **Intervention:** 修改表示会按预测改变行为吗？
- **Boundary:** 哪些反例暴露了碰撞或捷径？
- **Identifiability:** 是否存在多个同样解释数据、却语义不同的表示？

## Common Illusions

- “已经数字化”不等于“已经形成好表示”；
- “维度更多”不等于“信息更有用”；
- “距离更近”不等于“现实更相似”；
- “模型准确率高”不等于“表示捕获正确因素”；
- “Embedding 可视化成团”不等于“概念被理解”；
- “原始数据”不等于“没有经过人为选择”；
- “同一字段名”不等于“跨公司、跨时期语义一致”。

每项错觉都必须配更强测试：更换任务、打乱 ID、改变单位、检查时间边界、构造碰撞或跨分布迁移。

## Failure Modes

### Observation Blind Spot

现实中的关键因素从未被采集，模型无法通过更复杂架构补回。

### Representation Collision

任务相关的不同状态得到同一编码，例如 missing 与真实零值。

### False Geometry

类别编号、量纲或标准化方式制造没有语义依据的邻近关系。

### Leakage

未来信息、标签代理或结果变量进入输入表示，使离线表现虚高。

### Distribution Shift

训练时稳定的编码语义在新制度、地区或时期发生变化。

### Human Projection

研究者把可视化图案或相关方向命名成人类概念，却没有迁移、干预与边界证据。

## Mental Model Upgrade

### Before

```text
Representation
  = reality converted into numbers
```

### After

```text
Representation
  = observation boundary
  + encoding choice
  + geometry
  + available operations
  + declared information loss
```

升级完成的证据是：面对一个模型，读者不只问“输入数据是什么”，而会问模型能区分什么、什么被碰撞、距离代表什么，以及表示怎样限制下游学习。

## Learning Package Plan

### Notebook · Representation Geometry Lab

实现 weekday 的 ordinal、one-hot 与 cyclical encoding，计算距离并绘图；随后比较公司 raw features 与 standardized features 的近邻变化。每个实验必须先写语义预测。

### Understanding Audit

- **Explain:** 为什么表示不是现实副本或无害容器？
- **Predict:** 改变编码、单位或时间边界后，哪些距离与判断会改变？
- **Reconstruct:** 从空白页重建 Observation → Representation → Model 以及碰撞公式；
- **Transfer:** 为一个新领域设计两种任务不同、不可互换的表示。

### Capability Milestone

After completing the Learning Package, the learner can:

- **Explain:** separate reality, observation, representation, and model;
- **Predict:** identify how an encoding change alters geometry or available distinctions;
- **Build:** implement and compare several encodings for the same semantic object;
- **Read:** audit an AI or finance pipeline for collisions, leakage, and false geometry.

## Exercise Evidence

练习依次要求：识别表示边界、比较同一对象的多种编码、手算距离与碰撞、运行前预测编码扰动、审计公司特征向量，并设计一个能揭示 Shortcut 的跨分布测试。

## Connection and Bridge

Chapter 3 决定哪些关系值得保留；Chapter 4 决定这些关系以什么形式进入机器。表示一旦确定，系统能够执行的比较与变换也被部分确定。

但静态表示不会自己产生结果。像素不会自己识别对象，Token 不会自己形成句义，公司向量也不会自己给出预测。

> **如果表示规定了机器能够看见什么，那么有限的机械步骤怎样把一种表示可靠地变成另一种表示？**

这进入 Chapter 5：**为什么计算能够产生智能？**

## Scope Boundaries

本章不完整教授：

- 信息论与 rate-distortion；
- 统计充分性；
- Embedding 训练；
- latent space 与 manifold learning；
- VAE 和 disentanglement 方法；
- Tokenizer 算法；
- fairness representation learning；
- mechanistic interpretability。

这些内容只在服务“表示选择决定模型可见世界”时准确预览。

## Definition of Done

- [ ] Opening Story 清楚分离 Reality 与模型收到的遥测表示；
- [ ] Observation / Encoding / Distinction / Geometry / Operation 贯穿正文；
- [ ] 数学从编码图示自然进入映射、距离与碰撞；
- [ ] Notebook 让读者在运行前预测不同编码的几何后果；
- [ ] 工程部分不把 Representation 简化成 API 或数据类型；
- [ ] AI × Finance 证明“可比公司”依赖表示选择；
- [ ] Research Corner 准确说明归纳偏置与不可识别性；
- [ ] Common Illusions 均有更强检验；
- [ ] Bridge 使 Computation 成为下一个必要问题。

## Questions for Editorial Review

1. 火星遥测是否让 Reality / Observation / Representation 的区别足够直观？
2. 星期编码是否能在不过早教授向量空间的前提下建立几何直觉？
3. Observation / Encoding / Distinction / Geometry / Operation 是否适合作为全章统一审计框架？
4. (R:O\rightarrow Z)、碰撞与周期编码是否处于 Chapter 4 合适的数学深度？
5. 公司近邻案例是否真正迁移表示机制，而不是普通特征工程案例？
6. Research Corner 是否准确限制了“自动发现真实因素”的主张，又没有预支 Part III？
