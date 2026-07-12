# Chapter 12 Design Brief

**Working title:** 为什么矩阵能够描述变化？

**Book:** The AI Mind · Book I · Discovering Intelligence

**Author:** Codex

**Status:** Approved

**Source:** The existing Chapter 12 editorial merge supplies seed claims only.
The canonical chapter will be rewritten around the current Golden Chapter
Standard and the Chapter 11 transition.

## One Sentence

> **矩阵不是数字表格，而是一份变化契约：它说明每个输入坐标怎样共同贡献到每个输出坐标。**

## Knowledge Graph · Dependency Card

```text
Vector State
  → coordinate relationships across input and output
  → Matrix
      ├─ shape contract
      ├─ row = one output recipe
      ├─ column = one input influence
      ├─ matrix-vector product
      └─ composition order
  → Linear Transformation
```

### Need Before

- Chapter 10：数学必须声明 Object、Operation、Unit 与 Boundary；
- Chapter 11：Vector 是有语义的多属性状态；
- Vector Difference、Dot Product 与 Coordinate Order 的直觉。

### This Chapter

```text
input vector
  → relationship table
  → each output coordinate mixes all inputs
  → output vector
  → compose multiple changes
```

### Need After

- Chapter 13：什么变化是 Linear，为什么直线性与叠加如此重要；
- Chapter 14：为什么只有 Linear Transformation 不够；
- Chapter 15–19：梯度与 Backprop 怎样穿过多层变换。

## Book I Question

**本章的问题：** 一个 Vector 保存当前状态时，怎样用一份统一规则同时改变所有 Coordinate，并得到新的 Vector State？

**本章的回答：** 用 Matrix 声明 Input Space、Output Space 与每对 Coordinate 的贡献关系；Matrix-vector Product 让每一 Row 生成一个 Output，Composition 让变化形成 Pipeline。

**下一个问题：** Matrix 所描述的变化为什么具有可叠加、可预测的 Linear Structure，又有哪些关系无法由它单独表达？

## Core Question

为什么 Matrix Multiplication 不是“行乘列”的任意规定，而是把多个输入按每个输出的关系配方进行组合？Shape 为什么是语义契约，而不只是报错条件？

## Controlling Thesis

> **Matrix 是两个 Coordinate Systems 之间的关系模型：Rows 定义输出，Columns 追踪输入影响，乘法执行这份依赖契约，Composition 则组合变化。**

本章区分：

- Spreadsheet 不是 Transformation；
- Shape Match 不是 Semantic Match；
- Matrix Multiplication 不是 Elementwise Multiplication；
- Row/Column Order 不是排版；
- Composition 通常不能交换；
- Linear Layer 不是完整神经网络。

## Why This Chapter

Chapter 11 用 Vector 保存多个属性，但 Vector 是静态状态：

\[
\mathbf{x}=
[x_1,x_2,\ldots,x_n]^\top
\]

现在需要同时回答：

- 每个 Output 依赖哪些 Input？
- 依赖强度和方向是什么？
- Output 有多少维？
- 多步变化怎样组合？

若为每个 Output 手写一条独立公式，关系会散落。Matrix 把它们放进一个有 Shape、有 Coordinate Contract 的对象。

Without matrix reasoning, a learner cannot **interpret a linear layer, audit
shape and coordinate semantics, understand why multiplication mixes features,
or trace how composed transformations propagate state and error**.

## Starting Mental Model

```text
Matrix
  = a rectangular table of numbers
  = many vectors stacked together
  = row times column procedure
```

升级为：

```text
Matrix
  = input-output coordinate contract
  + one row per output recipe
  + one column per input influence
  + shape and unit semantics
  + composable transformation
```

## Learning Objectives

完成本章后，读者能够：

1. 区分 Number Table、Dataset Table 与 Transformation Matrix；
2. 使用 Matrix Transformation Audit；
3. 解释 $m\times n$ Shape 的 Input/Output 含义；
4. 从一组 Output Equation 构造 Matrix；
5. 从 Matrix Row 和 Column 恢复关系语义；
6. 手算 Matrix-vector Product 并用两种视角解释；
7. 解释 Identity、Scaling、Mixing 与 Projection-like Examples；
8. 预测 Transpose、Order Drift、Unit Mismatch 与 Shape Error；
9. 解释 Matrix Composition 的顺序；
10. 为 Factor Exposure 或 Neural Layer 建立 Shape Contract。

## Opening Story · 三支麦克风，两个扬声器

一场小型演出有三支麦克风：主唱、吉他、鼓。场地有左右两个扬声器。

音响工程师必须决定：

- 左扬声器接收多少主唱、吉他和鼓；
- 右扬声器接收多少主唱、吉他和鼓。

输入状态：

```text
[vocal, guitar, drums]
```

输出状态：

```text
[left speaker, right speaker]
```

每个 Speaker 都是一份 Input Mix Recipe：

```text
left  = 0.8*vocal + 0.5*guitar + 0.3*drums
right = 0.8*vocal + 0.4*guitar + 0.6*drums
```

两份 Recipe 可以整齐放入一个 Matrix。Rows 对应两个 Output，Columns 对应三个 Input。

Matrix 不是让音乐变成表格，而是保存“哪些输入怎样共同形成每个输出”的关系。

故事边界：真实音频混音还包含时间、频率、非线性失真和反馈。本例只隔离 Input-output Mixing。

## Feynman Model · 每一行是一张配方卡

厨房有三种原料，准备两种饮料。

- 配方卡 1 写第一杯如何混合三种原料；
- 配方卡 2 写第二杯如何混合三种原料。

把配方卡叠起来，就是 Matrix。

```text
row    → one output recipe
column → one ingredient's influence across outputs
Ax     → execute every recipe on the same input
```

配方类比有边界：有些现实混合不是线性的，例如化学反应与饱和。Matrix 只先描述可按比例叠加的关系。

## First-Principles Spine · Matrix Transformation Audit

| Element | 核心问题 | 缺失时的失败 |
|---|---|---|
| Input Object | $mathbf{x}$ 描述什么？ | 输入无语义 |
| Output Object | $mathbf{y}$ 描述什么？ | 结果无法解释 |
| Shape | $m\times n$ 对应哪些空间？ | 只为通过报错 |
| Rows | 每个 Output 怎样混合 Input？ | 公式无法恢复 |
| Columns | 一个 Input 影响哪些 Output？ | 影响路径不可追踪 |
| Units | Entry 的单位怎样转换？ | 数值合法、量纲错误 |
| Operation | 为什么使用 $A\mathbf{x}$？ | 机械行列乘法 |
| Composition | 多个变化顺序是什么？ | Pipeline 语义颠倒 |
| Boundary | 哪些非线性或丢失未表达？ | Matrix 被当成现实 |

Audit 从 Input/Output Object 开始，不从矩阵数字开始。

## From Equations to Matrix

麦克风例子：

\[
y_1=0.8x_1+0.5x_2+0.3x_3
\]

\[
y_2=0.8x_1+0.4x_2+0.6x_3
\]

写成：

\[
\mathbf{y}=A\mathbf{x}
\]

其中：

\[
A=
\begin{bmatrix}
0.8&0.5&0.3\\
0.8&0.4&0.6
\end{bmatrix},
\quad
\mathbf{x}\in\mathbb{R}^{3},
\quad
\mathbf{y}\in\mathbb{R}^{2}
\]

所以：

\[
A\in\mathbb{R}^{2\times3}
\]

Shape 的语义是：三个 Input Coordinate 进入，两个 Output Coordinate 产生。

## Two Views of Matrix-vector Multiplication

### Row View · 每个 Output 一次 Dot Product

\[
y_i=\mathbf{a}_i^{\top}\mathbf{x}
\]

第 $i$ Row 是第 $i$ 个 Output 的 Recipe。

### Column View · 每个 Input 贡献一个 Output Direction

\[
A\mathbf{x}
=x_1\mathbf{a}^{(1)}+x_2\mathbf{a}^{(2)}+\cdots+x_n\mathbf{a}^{(n)}
\]

第 $j$ Column 说明 Input $x_j$ 同时怎样影响所有 Output。

Row View 适合回答“一个 Output 怎么算”；Column View 适合回答“一个 Input 的影响流向哪里”。

## Four Transparent Matrices

### Identity

\[
I\mathbf{x}=\mathbf{x}
\]

保持状态，是 Composition 的基准。

### Scaling

Diagonal Matrix 分别缩放 Coordinate。

\[
\begin{bmatrix}2&0\\0&0.5\end{bmatrix}
\begin{bmatrix}x_1\\x_2\end{bmatrix}
\]

### Mixing

Off-diagonal Entry 让一个 Output 依赖多个 Input。

### Information-dropping Map

从三维到二维的 Matrix 可以丢失某些方向。这里仅建立 Information Boundary，不提前教授 Rank 或 Null Space 理论。

## Composition · 变化为什么有顺序？

先执行 $A$，再执行 $B$：

\[
\mathbf{z}=B(A\mathbf{x})=(BA)\mathbf{x}
\]

$BA$ 的右侧 $A$ 先作用。

通常：

\[
BA\ne AB
\]

原因不是规则任性，而是第二个变化接收第一个变化产生的 Coordinate System。缩放后旋转，与旋转后沿原轴缩放，结果可能不同。

本章只建立 Composition Order，不进入完整 Matrix-matrix 计算技巧。

## Visualization Spine · Grid Before and After

二维网格依次经过：

1. Identity；
2. Axis Scaling；
3. Shear-like Mixing；
4. Dimension Reduction Preview。

图示同时标出：Input Basis Vector 的去向、Output Axis 与一个测试 Vector。

目标不是背 Transformation 名称，而是看到 Matrix 通过改变 Basis Direction 影响整个空间中的 Vector。

## Coding Lab · Rows Build Outputs, Columns Trace Influence

NumPy Lab 先用显式 Equation，再用 `A @ x`：

```python
y_manual = np.array([
    0.8*x[0] + 0.5*x[1] + 0.3*x[2],
    0.8*x[0] + 0.4*x[1] + 0.6*x[2],
])

y_matrix = A @ x
```

Perturbation Tests：

1. 只提高一支麦克风，预测哪些 Output 变化；
2. 交换两个 Input Coordinate，但不交换 Column；
3. 交换 Row，观察 Output Label 是否同步；
4. 转置 Matrix，解释 Shape 与语义变化；
5. 把一个 Entry 的 Unit 放大 1000 倍；
6. 比较 $BA\mathbf{x}$ 与 $AB\mathbf{x}$；
7. 删除一个 Output Row，记录 Information Boundary。

重点是预测关系传播，不是熟悉 `@`。

## Engineering Perspective · Shape 是接口，不是完整语义

Linear Layer 常写：

\[
\mathbf{y}=W\mathbf{x}+\mathbf{b}
\]

若 $W\in\mathbb{R}^{m\times n}$，则 Input Width 为 $n$，Output Width 为 $m$。

Shape Contract 能发现很多错误，但发现不了：

- Feature Order Drift；
- Unit Mismatch；
- Wrong Model Version；
- Row Label 与 Output Label 不一致；
- Batch/Feature Axis 语义交换但 Shape 恰好兼容。

工程 Schema 必须保存 Input/Output Name、Order、Unit、Version 与 Expected Range。

## AI × Finance · Factor Exposure Matrix 是关系表

三家公司暴露于 Growth、Rates 与 FX：

\[
E=
\begin{bmatrix}
e_{11}&e_{12}&e_{13}\\
e_{21}&e_{22}&e_{23}\\
e_{31}&e_{32}&e_{33}
\end{bmatrix}
\]

若 Scenario Vector 为：

\[
\mathbf{s}=
[\Delta\text{growth},\Delta\text{rates},\Delta\text{FX}]^\top
\]

则：

\[
\Delta\mathbf{r}=E\mathbf{s}
\]

Rows 是每家公司的 Scenario Recipe；Columns 是某个 Factor 对所有公司的影响。

这不是收益真值。Exposure、Linear Assumption、Time Horizon、Interaction 与 Regime 都是 Boundary。

Finance Lab 要求从 Scenario Equation 建 Matrix，再用 Row/Column View 审计结果；不能只把历史 Regression Coefficient 当永久机制。

## Research Corner · Matrix Structure 是 Inductive Bias

本节只提出：

1. Dense Matrix 与 Sparse/Structured Matrix 假设了什么关系？
2. 为什么参数共享可以减少自由度并改变 Generalization？
3. Low-rank Structure 何时是有用压缩，何时丢失关键方向？

候选阅读路标聚焦 Structured Linear Maps 与 Parameter Sharing，正文前核验 2–3 个原始来源。不提前教授 CNN、LoRA、SVD 或完整 Rank Theory。

## Common Illusions

- “矩阵是表格”不等于它描述 Transformation；
- “Shape 能乘”不等于语义匹配；
- “行列乘法记住了”不等于理解依赖；
- “更多参数”不等于更好 Transformation；
- “Transpose”不等于简单换排版；
- “$AB=BA$”通常不成立；
- “Linear Layer”不等于完整 Neural Network；
- “输出维度更高”不等于信息更多。

## Failure Modes

### Row/Column Drift

Coordinate 顺序变化，Matrix 未同步。

### Shape-only Validation

尺寸通过，语义错误。

### Transpose Confusion

Input/output 角色被颠倒。

### Unit Propagation Failure

Entry 单位无法把 Input 转成 Output。

### Composition-order Error

Pipeline 变化顺序颠倒。

### Hidden Information Loss

降维后把丢失方向当成可恢复。

### Dense-by-default

默认所有 Input 影响所有 Output，引入不必要关系。

### Nonlinearity Blindness

用单个 Matrix 表达饱和、阈值或交互规则。

## Mental Model Upgrade

### Before

```text
Matrix = rectangular number table + row times column
```

### After

```text
Matrix = input-output coordinate contract
         + output recipes in rows
         + input influence paths in columns
         + shape and unit semantics
         + ordered composition
         + explicit information boundary
```

升级完成的证据是：读者能从 Matrix 恢复 Equation，也能从 Equation 构造 Matrix，并预测改动一个 Row、Column 或 Composition Order 的后果。

## Learning Package Plan

### Notebook · Mix, Trace, Compose

从麦克风 Mixing 开始，比较 Manual Equation 与 `A @ x`，执行 Row/Column、Transpose、Unit 与 Composition Perturbation。

### Figure Set

1. Input-output Mixing Contract；
2. Row Recipe vs Column Influence；
3. Shape as Space Mapping；
4. Composition Order on a Grid。

### Understanding Audit

- **Explain:** 为什么 Matrix-vector Product 是 Output Recipe？
- **Predict:** 改 Row、Column、Transpose 或 Order 后会怎样？
- **Reconstruct:** 从 Equation 构造 Matrix，再恢复 Equation；
- **Transfer:** 为 Audio、Feature Layer 或 Finance Scenario 建 Matrix Contract。

### Capability Milestone

- **Explain:** interpret shape, rows, columns, and composition;
- **Predict:** trace input influence and transformation failures;
- **Build:** create and test a matrix transformation contract;
- **Read:** identify semantic errors that shape checks miss.

## Exercise Evidence

练习依次要求：从 Equation 建 Matrix、手算 $A\mathbf{x}$、双视角解释、追踪 Column Influence、审计 Units、预测 Composition Order、构建 Factor Exposure Matrix，并从错误 Output 反推 Row/Column Failure。

## Connection and Bridge

Chapter 11 让多属性状态进入 Vector；Chapter 12 用 Matrix 描述状态之间的系统变化。

但并非所有变化都能由单个 Matrix 精确表达。Matrix Transformation 保留叠加关系，而现实中常有阈值、饱和与条件切换。

> **什么使一种变化成为 Linear Transformation？为什么这种限制既强大，又不足以表达全部智能？**

这进入 Chapter 13：**为什么线性变化能够解决复杂问题？**

## Scope Boundaries

本章不完整教授：

- Determinant 与 Inverse；
- Rank、Null Space 与 Column Space 理论；
- Eigenvalue、SVD 与 Basis Change；
- CNN、Attention、LoRA；
- 完整 Matrix-matrix 算法；
- Batch Matrix Multiplication；
- 自动微分。

这些内容只在服务“Input-output Transformation Contract”时准确预览。

## Definition of Done

- [ ] Opening Story 让 Matrix 成为多 Input 到多 Output 的必要关系表；
- [ ] Matrix Transformation Audit 贯穿数学、Lab、工程与 Finance；
- [ ] Row View 与 Column View 都能解释 $A\mathbf{x}$；
- [ ] Shape 始终连接 Input/Output Space；
- [ ] Composition 强调顺序与语义；
- [ ] Engineering 区分 Shape Match 与 Semantic Match；
- [ ] Finance 使用 Factor Exposure Matrix，明确模型边界；
- [ ] Bridge 自然制造 Linear Transformation 问题。

## Questions for Editorial Review

1. 麦克风到扬声器是否自然建立多 Input 到多 Output 的 Matrix 需求？
2. Input / Output / Shape / Rows / Columns / Units / Operation / Composition / Boundary 是否适合作为统一 Matrix Audit？
3. Row View 与 Column View 是否足够建立 Multiplication 直觉？
4. Identity、Scaling、Mixing 与 Information-dropping Preview 是否处于合适深度？
5. Composition 是否讲清顺序但没有提前变成 Matrix-matrix 技巧课？
6. Factor Exposure Matrix 是否专业且可迁移？
7. Chapter 13 Bridge 是否自然产生 Linear Transformation 的必要问题？
