# Chapter 11 Design Brief

**Working title:** 为什么向量比数字更适合描述世界？

**Book:** The AI Mind · Book I · Discovering Intelligence

**Author:** Codex

**Status:** Approved

**Source:** The existing Chapter 11 editorial merge supplies seed claims only.
The canonical chapter will be rewritten around the current Golden Chapter
Standard and the Chapter 10 transition.

## One Sentence

> **向量不是一串数字，而是一个对象在选定坐标系中的位置；它让多个属性及其关系同时进入计算。**

## Knowledge Graph · Dependency Card

```text
Mathematical Language
  → one scalar cannot preserve multiple independent attributes
  → Vector
      ├─ coordinates
      ├─ direction
      ├─ magnitude
      ├─ distance
      └─ similarity
  → Matrix as transformation between vector states
```

### Need Before

- Chapter 3：抽象保留任务相关关系；
- Chapter 4：表示决定机器可以区分什么；
- Chapter 10：数学关系必须声明 Object、Unit、Operation 与 Boundary。

### This Chapter

```text
multi-attribute object
  → ordered coordinates
  → vector position
  → geometry chosen by scale and metric
  → comparison and transformation readiness
```

### Need After

- Chapter 12：Matrix 怎样同时重组多个 Vector Coordinate；
- Chapter 13：Linear Transformation 怎样改变方向与尺度；
- Part III：Embedding、Attention 与 Learned Representation。

## Book I Question

**本章的问题：** 当一个对象拥有多个可以独立变化的属性时，怎样在不立刻压成单一 Score 的情况下保存并比较它？

**本章的回答：** 选择有语义、有顺序、有单位的 Coordinate，把对象表示为 Vector，再明确 Scale、Origin 与 Metric，使位置、方向和距离服务具体任务。

**下一个问题：** 如果 Vector 保存一个状态，什么数学对象能够系统地把它变成另一个状态？

## Core Question

为什么“很多数字排在一起”仍不足以成为有意义的 Vector？Coordinate、Order、Scale 与 Metric 如何决定 Geometry，又怎样避免把距离误认为现实中的天然相似？

## Controlling Thesis

> **Vector 的力量不来自数字数量，而来自一份坐标契约：每个位置代表什么、如何缩放、允许怎样比较，以及这种 Geometry 在什么任务边界内有意义。**

本章区分：

- Identifier 不是 Description；
- Number List 不是 Semantic Vector；
- Distance 不是天然 Similarity；
- Coordinate Order 不是排版细节；
- High Dimension 不是 Rich Understanding；
- Embedding 不是现实意义的唯一发现。

## Why This Chapter

一个数字可以回答一个问题：温度是多少？价格是多少？年龄是多少？

但一家公司、一名病人、一张图片或一个 Token 同时拥有多个属性。把它们过早压成一个 Score，会让不同对象发生 Representation Collision。

```text
company A: high growth, low margin
company B: low growth, high margin
same scalar score
```

Vector 暂时保留这些差异，使后续计算可以选择怎样组合它们。

Without vector reasoning, a learner cannot **represent a multi-attribute
state, interpret geometric operations, audit feature scaling, or understand
why matrices and embeddings operate on coordinates rather than isolated
numbers**.

## Starting Mental Model

```text
Vector
  = a list of numbers
  = an arrow
  = more information than one number
```

升级为：

```text
Vector
  = ordered coordinates
  + declared semantics and units
  + chosen origin and scale
  + task-relevant geometry
  + explicit information boundary
```

## Learning Objectives

完成本章后，读者能够：

1. 区分 Scalar、Identifier、Tuple 与 Vector；
2. 使用 Coordinate Contract 审计 Vector 表示；
3. 解释 Coordinate Order、Unit、Scale 与 Origin；
4. 从现实对象建立二维与三维 Vector；
5. 解释 Vector Addition 与 Scalar Multiplication 的语义；
6. 计算并解释 Magnitude、Distance、Dot Product 与 Cosine Similarity；
7. 预测 Feature Scaling 如何改变最近邻；
8. 识别 Representation Collision、Distance Concentration 与 Metric Mismatch；
9. 构建并审计 Company Vector；
10. 说明为什么 Matrix 是 Vector Transformation 的自然下一步。

## Opening Story · 同样 72 分的两家公司

一套投资筛选系统给两家公司都打了 72 分。

公司 A：

- Revenue Growth 很高；
- Margin 很低；
- Debt 很高；
- Valuation 较便宜。

公司 B：

- Growth 较低；
- Margin 很高；
- Balance Sheet 很强；
- Valuation 较贵。

一个 Score 把不同结构压成同一个位置。若任务只是排序，它可能有用；若要判断利率上升、需求下降或竞争加剧时谁更脆弱，72 分已经丢失关键关系。

团队保留四个 Coordinate：

```text
[growth, margin, leverage, valuation]
```

现在两家公司不再是同一个数字，而是多维空间中的两个位置。压力测试可以沿“利率”“需求”或“定价权”方向观察变化。

故事边界：Vector 仍然是选择后的表示。没有进入 Coordinate 的管理层、制度和竞争动态不会凭空保留。

## Feynman Model · 地址为什么不只写一个数字？

朋友说他住在“25”。你无法找到他。

一份地址需要城市、街道、门牌、楼层和房间号。每个位置有固定含义，顺序也不能随意交换。

```text
[city, street, building, floor, room]
```

Vector 也一样：它不是数字袋子，而是 Coordinate Contract。

地址类比有边界：地址 Coordinate 常是类别，不一定支持加法和距离。数学 Vector 的 Coordinate 必须与允许的 Operation 一起解释。

## First-Principles Spine · Vector Representation Audit

| Element | 核心问题 | 缺失时的失败 |
|---|---|---|
| Object | Vector 描述谁或什么？ | 数字失去对象 |
| Coordinates | 每一维代表什么？ | 列表无语义 |
| Order | 第 $i$ 位为何固定？ | 交换后对象改变 |
| Unit and Scale | 各维如何测量与标准化？ | 某维支配 Geometry |
| Origin and Basis | 零点和方向如何选择？ | 位置含义模糊 |
| Operation | Addition、Distance、Dot Product 是否有语义？ | 合法计算，无效结论 |
| Metric | 哪种差异代表任务相似？ | 最近邻误导 |
| Boundary | 哪些信息未被表示？ | Vector 被当成现实 |

Audit 必须从任务开始，而不是从 Dimension 数量开始。

## From Attributes to Notation

一家公司用三个 Coordinate 表示：

\[
\mathbf{x}=
\begin{bmatrix}
x_1\\
x_2\\
x_3
\end{bmatrix}
=
\begin{bmatrix}
\text{growth}\\
\text{margin}\\
\text{leverage}
\end{bmatrix}
\]

更一般地：

\[
\mathbf{x}\in\mathbb{R}^d
\]

表示 $mathbf{x}$ 有 $d$ 个实数 Coordinate。$mathbb{R}^d$ 声明数值类型与 Dimension，不自动声明每一维语义。

## Geometry Begins with a Contract

### Position

Vector 是对象在选定 Coordinate System 中的位置。

### Difference

\[
\mathbf{b}-\mathbf{a}
\]

表示从 A 到 B 的 Coordinate Change。只有单位与语义兼容时，差值才有意义。

### Addition

\[
\mathbf{x}+\Delta\mathbf{x}
\]

可表示状态加上变化，例如 Growth 与 Margin 同时改变。

### Scalar Multiplication

\[
c\mathbf{x}
\]

把所有 Coordinate 按同一 Scalar 缩放。现实语义必须单独检查；把公司所有属性乘二未必有经济意义。

### Magnitude

\[
\lVert\mathbf{x}\rVert_2
=\sqrt{\sum_{i=1}^{d}x_i^2}
\]

Magnitude 是相对于 Origin 的长度，不自动等于“对象大小”。

### Distance

\[
d(\mathbf{x},\mathbf{y})
=\lVert\mathbf{x}-\mathbf{y}\rVert_2
\]

Distance 依赖 Coordinate、Unit、Scale 与 Metric。收入以美元计而 Margin 以百分比计时，未经处理的 Euclidean Distance 可能几乎只看收入。

### Dot Product and Direction

\[
\mathbf{x}^{\top}\mathbf{y}
=\sum_{i=1}^{d}x_i y_i
\]

Dot Product 同时受 Magnitude 与方向影响。它可以度量 Alignment，但必须说明 Coordinate Geometry。

### Cosine Similarity

\[
\cos\theta=
\frac{\mathbf{x}^{\top}\mathbf{y}}
{\lVert\mathbf{x}\rVert\lVert\mathbf{y}\rVert}
\]

Cosine 关注方向，弱化整体尺度。它不是永远优于 Distance，只回答不同问题。

## Visualization Spine · 同一对象的三种 Geometry

用二维 Company Vector 展示：

1. Raw Scale：Revenue 支配横轴；
2. Standardized Scale：Growth 与 Margin 可比较；
3. Task-weighted Scale：风险任务放大 Leverage。

同一批公司会产生不同最近邻。图示目的不是找“真实 Geometry”，而是让读者看见 Geometry 来自表示与任务选择。

## Coding Lab · Scale Can Change Your Nearest Neighbor

NumPy Lab：

```python
companies = np.array([
    [revenue, growth, margin],
    ...
])
```

实验顺序：

1. 运行前预测 Raw Distance 的主导维度；
2. 计算 Euclidean Distance；
3. Standardize 每个 Coordinate；
4. 重新计算最近邻；
5. 比较 Cosine Similarity；
6. 改变 Task Weight；
7. 删除一个 Coordinate，记录 Information Boundary。

Perturbation Tests：交换 Coordinate Order、改变 Unit、添加无关高方差特征、重复相同特征、加入 Missing Value。

目标不是使用 NumPy API，而是预测 Geometry 怎样随 Contract 改变。

## Engineering Perspective · Feature Vector 是接口

生产系统中的 Feature Vector 必须有 Schema：

- Feature Name；
- Position；
- Type；
- Unit；
- Normalization；
- Missing-value Policy；
- Timestamp 与 Point-in-time Availability；
- Version。

训练与推理 Coordinate Order 不一致，会产生数值合法、语义错误的 Silent Failure。

Vector Database 中的 Embedding 也不是“存进去就能相似搜索”。必须声明模型版本、Normalization、Metric、Index 与 Query/Document 是否在兼容空间。

## AI × Finance · 可比公司是 Geometry Claim

Company Vector 可以包含：

\[
\mathbf{x}
=
[\text{growth},\text{margin},\text{ROIC},\text{leverage},\text{valuation}]
\]

但“可比”取决于任务：

- Earnings Forecast 可能重视 Growth 与 Margin；
- Credit Risk 可能重视 Leverage 与 Cash Flow；
- Long-term Quality 可能重视 ROIC 与 Reinvestment；
- Valuation Relative 可能重视 Accounting 与 Industry Boundary。

Nearest Neighbor 不是发现天然同行，而是在某套 Coordinate、Scale 与 Metric 下执行一项相似性主张。

Finance Lab 要求先写 Comparable-company Contract，再看最近邻。禁止先看结果后调整 Weight 直到出现喜欢的公司。

## Research Corner · Learned Geometry 是否更真实？

本节只提出三个问题：

1. Learned Embedding 的距离是否稳定对应任务关系？
2. 高维空间中的 Distance 是否仍有直觉意义？
3. 同一模型的不同层、不同训练目标是否产生不同 Geometry？

候选阅读路标聚焦 Distributional Representation、Embedding Geometry 与 High-dimensional Distance。正文前核验 2–3 个原始来源，不提前讲 Word2Vec、Transformer 或完整 Curse of Dimensionality。

## Common Illusions

- “数字更多”不等于表示更完整；
- “Dimension 更高”不等于理解更深；
- “Distance 更近”不等于现实更相似；
- “Coordinate 可交换”不等于 Order 无意义；
- “Normalize 后公平”不等于 Metric 合理；
- “Cosine 高”不等于语义相同；
- “Learned Embedding”不等于发现唯一意义空间；
- “Vector Database”不等于可靠 Retrieval。

## Failure Modes

### Coordinate Collision

不同对象进入同一 Vector。

### Order Drift

训练与推理 Feature 顺序不一致。

### Unit Dominance

大数值 Coordinate 支配 Distance。

### Metric Mismatch

使用的 Geometry 不对应任务相似性。

### Redundant Dimension

重复特征被无意多次加权。

### Missingness Erasure

填充值隐藏“缺失本身”的信息。

### High-dimensional Noise

无关 Dimension 累积，距离失去区分力。

### Semantic Overclaim

把模型空间的邻近解释成现实本质。

## Mental Model Upgrade

### Before

```text
Vector = an arrow or a list of numbers
```

### After

```text
Vector = ordered coordinates
         + semantics and units
         + origin and scale
         + task-relevant operations
         + explicit information boundary
```

升级完成的证据是：读者能预测改变 Scale、Order 或 Metric 后，Geometry 和结论怎样变化。

## Learning Package Plan

### Notebook · Build, Scale, Compare

创建二维与三维 Company Vector，比较 Raw、Standardized、Task-weighted Geometry，并执行 Order、Unit 与 Noise Perturbation。

### Figure Set

1. Scalar Collision vs Vector Separation；
2. Coordinate Contract；
3. Raw vs Standardized Nearest Neighbors；
4. Direction vs Magnitude。

### Understanding Audit

- **Explain:** 为什么 Number List 不自动成为有意义 Vector？
- **Predict:** Scale、Order、Metric 改变怎样影响结果？
- **Reconstruct:** 从现实对象重建 Coordinate Contract 与公式；
- **Transfer:** 为图像、文本、医疗或 Finance 设计 Vector 表示。

### Capability Milestone

- **Explain:** interpret vector coordinates, geometry, and boundaries;
- **Predict:** audit scaling and metric changes before computation;
- **Build:** construct and test a versioned feature-vector contract;
- **Read:** identify when embedding similarity overclaims meaning.

## Exercise Evidence

练习依次要求：区分 Scalar/Identifier/Vector、手算 Vector Operation、执行 Distance 与 Cosine、预测 Scale Perturbation、审计 Feature Schema、设计 Company Vector，并从错误最近邻反推 Contract Failure。

## Connection and Bridge

Chapter 10 说明数学让关系进入可计算语言；Chapter 11 提供第一个保存多属性状态的数学对象。

但 Vector 只是一个位置或状态。它不会自己改变 Coordinate、旋转方向、组合 Feature 或产生新表示。

> **如果向量保存状态，什么数学对象能够一次描述所有 Coordinate 怎样共同变化？**

这进入 Chapter 12：**为什么矩阵能够描述变化？**

## Scope Boundaries

本章不完整教授：

- Vector Space Axiom；
- Basis Change 与 Eigenvector；
- Matrix Multiplication；
- Word2Vec 或 Transformer Embedding；
- 高维统计理论；
- Vector Database 系统实现；
- 全部 Distance Metric 目录。

这些内容只在服务“多属性表示与任务 Geometry”时准确预览。

## Definition of Done

- [ ] Opening Story 让 Scalar Collision 自然制造 Vector 需求；
- [ ] Vector Representation Audit 贯穿正文、Lab 与 Finance；
- [ ] 数学解释 Position、Difference、Magnitude、Distance 与 Direction；
- [ ] Scale Perturbation 改变最近邻，且读者先预测；
- [ ] Feature Vector 作为版本化工程接口；
- [ ] Finance 把 Comparable Company 明确为 Geometry Claim；
- [ ] Research Corner 不提前变成 Embedding 课程；
- [ ] Bridge 让 Matrix 成为 Vector Transformation 的自然答案。

## Questions for Editorial Review

1. Company Score Collision 是否是 Vector 需求的自然 Opening？
2. Object / Coordinates / Order / Unit and Scale / Origin and Basis / Operation / Metric / Boundary 是否适合作为统一 Vector Audit？
3. Magnitude、Distance、Dot Product 与 Cosine 是否在 Chapter 11 合适深度？
4. 地址类比是否清楚说明 Coordinate Contract，同时准确标出类别地址的边界？
5. Scale Lab 是否真正培养 Geometry 直觉，而不是 NumPy 操作？
6. Comparable-company Geometry 是否提供专业且可迁移的 Finance 案例？
7. Chapter 12 Bridge 是否自然制造 Matrix Transformation 需求？
