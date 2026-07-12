# Chapter 13 Design Brief

**Working title:** 为什么线性变化能够解决复杂问题？

**Book:** The AI Mind · Book I · Discovering Intelligence

**Author:** Codex

**Status:** Awaiting Editor-in-Chief review

**Source:** The existing Chapter 13 v1.0 supplies seed explanations only. The
canonical rewrite will use the current Golden Chapter Standard and distinguish
strict Linear Transformation from Affine maps precisely.

## One Sentence

> **线性不是“看起来像直线”，而是一份叠加契约：输入可以拆分、缩放和重组，输出仍以同样方式响应。**

## Knowledge Graph · Dependency Card

```text
Vector State
  → Matrix Transformation Contract
  → Superposition Test
      ├─ additivity
      └─ homogeneity
  → Linear Transformation
      ├─ basis determines all inputs
      ├─ composition remains linear
      └─ residual reveals boundary
  → Nonlinearity
```

### Need Before

- Chapter 11：Vector 是 Coordinate State；
- Chapter 12：Matrix 执行 Input-output Transformation；
- Row/Column View、Composition Order 与 Information Boundary。

### This Chapter

```text
transformation
  → test additivity
  → test homogeneity
  → inspect origin and basis response
  → exploit decomposition and composition
  → measure residual and boundary
```

### Need After

- Chapter 14：阈值、饱和、弯曲与交互为何要求 Nonlinearity；
- Chapter 15：当输出变化时，Gradient 怎样描述局部敏感性；
- Deep Learning：Linear/Affine 与 Nonlinear Operation 的交替组合。

## Book I Question

**本章的问题：** 什么使一种 Matrix Transformation 成为 Linear？为什么这种限制让变化可预测、可分解、可组合，同时又限制表达力？

**本章的回答：** Linear Transformation 保持 Addition 与 Scalar Multiplication；因此只要知道 Basis 的去向，就能重建全部输入的变化，且多层 Composition 仍属于同一结构。

**下一个问题：** 如果 Linear/Affine Composition 仍可压成一次变化，系统怎样表达阈值、饱和、弯曲和条件切换？

## Core Question

Superposition 为什么是 Linear 的本质，而“直线图像”只是结果之一？Bias 为什么使 `Wx+b` 成为 Affine？Residual 又怎样告诉我们 Linear Model 在哪里失效？

## Controlling Thesis

> **Linear Transformation 的力量来自可预测限制：整体响应可以由部分响应重建，复杂输入可以由 Basis Response 组合，多步变化仍可压缩；它的边界也正来自同一限制。**

本章区分：

- Linear Function 不是日常语言中的“近似直线”全部含义；
- $W\mathbf{x}$ 是 Linear，$W\mathbf{x}+\mathbf{b}$ 严格说是 Affine；
- Matrix Representation 不自动保证现实机制 Linear；
- Good Fit 不自动证明 Superposition；
- 多层 Linear/Affine 不自动增加表达类别；
- Linear Baseline 简单不等于无用。

## Why This Chapter

Chapter 12 说明 Matrix 怎样执行变化，却没有回答：哪些变化可以由 Matrix 在所有输入上稳定描述？

Linear Structure 提供一个强大承诺：

```text
response to combined input
  = combined responses to each input
```

若承诺成立，我们不必分别测量无限多个输入。只要知道 Basis Direction 的响应，就能推导任意组合。

Without linear reasoning, a learner cannot **test superposition, distinguish
Linear from Affine behavior, understand why basis responses determine a map,
or explain why stacked linear layers collapse without nonlinearity**.

## Starting Mental Model

```text
Linear
  = a straight line
  = simple relationship
  = y = wx + b
```

升级为：

```text
Linear Transformation
  = additivity
  + homogeneity
  + origin preservation
  + basis-determined behavior
  + composability
  + explicit residual boundary
```

并单独保留：

```text
Affine map = Linear Transformation + translation
```

## Learning Objectives

完成本章后，读者能够：

1. 用 Superposition 而非视觉印象定义 Linear；
2. 使用 Linear Transformation Audit；
3. 检验 Additivity 与 Homogeneity；
4. 推导 $T(\mathbf{0})=\mathbf{0}$；
5. 区分 $W\mathbf{x}$ 与 $W\mathbf{x}+\mathbf{b}$；
6. 从 Basis Response 重建任意输入的 Output；
7. 解释为什么 Linear Composition 仍然 Linear；
8. 用 Residual 与 Perturbation 找出 Linear Boundary；
9. 建立并审计 Finance Factor Baseline；
10. 解释为什么 Deep Network 需要 Nonlinearity。

## Opening Story · 传感器什么时候可以相信“加起来”？

实验室用光学传感器测量溶液浓度。

低浓度范围内：

- 浓度加倍，读数也近似加倍；
- 两份样本的光学贡献合在一起，读数近似等于各自读数之和。

工程师因此能用少量 Calibration Point 推导许多输入。

但浓度继续上升后，传感器开始 Saturate：输入加倍，读数不再加倍。原来的 Matrix 仍能计算，Superposition Contract 已经失效。

这个故事展示两件事：

1. Linearity 是可以实验检验的响应结构；
2. Linear Model 通常有适用范围，而不是现实的永久机制。

故事边界：真实光学定律与仪器误差更复杂。本例只隔离 Additivity、Homogeneity 与 Saturation。

## Feynman Model · 一台遵守叠加规则的放大器

想象一台透明放大器。

- 把 Signal A 和 B 先合并再放大；
- 分别放大 A 和 B，再把结果合并。

若两种方式总得到相同结果，它满足 Additivity。

再把 Input 放大 3 倍。若 Output 也正好放大 3 倍，它满足 Homogeneity。

```text
T(a + b) = T(a) + T(b)
T(ca)    = cT(a)
```

放大器类比有边界：真实设备会有 Noise、Clipping 与 Frequency Response。恰恰是这些偏离帮助我们看到 Linear Boundary。

## First-Principles Spine · Linear Transformation Audit

| Element | 核心问题 | 缺失时的失败 |
|---|---|---|
| Input/Output Space | Transformation 连接什么对象？ | 公式无语义 |
| Additivity | 合并输入是否等于合并响应？ | 交互被隐藏 |
| Homogeneity | 缩放输入是否同比缩放输出？ | Saturation 被忽略 |
| Origin | $T(0)$ 是否为 $0$？ | Affine 被误称 Linear |
| Basis Response | Basis 去向能否决定全部输入？ | 无法重建 Map |
| Composition | 多步变化是否保持结构？ | Depth 被误解 |
| Residual | 观察与 Linear Prediction 差多少？ | Boundary 不可见 |
| Boundary | 哪个范围、Regime 与任务成立？ | 局部关系被永久化 |

Audit 将“Linear”从标签变成一组可运行测试。

## Mathematics · Superposition Is the Definition

对于 Transformation $T$：

\[
T(\mathbf{u}+\mathbf{v})
=T(\mathbf{u})+T(\mathbf{v})
\]

\[
T(c\mathbf{u})
=cT(\mathbf{u})
\]

合并为：

\[
T(a\mathbf{u}+b\mathbf{v})
=aT(\mathbf{u})+bT(\mathbf{v})
\]

令 $c=0$：

\[
T(\mathbf{0})=\mathbf{0}
\]

因此任何不保持 Origin 的 Map 都不是严格 Linear。

## Linear vs Affine · Bias 去哪里了？

严格 Linear：

\[
T(\mathbf{x})=W\mathbf{x}
\]

Affine：

\[
f(\mathbf{x})=W\mathbf{x}+\mathbf{b}
\]

Bias 平移整个 Output，所以通常：

\[
f(\mathbf{0})=\mathbf{b}\ne\mathbf{0}
\]

PyTorch 的 `nn.Linear` 实际通常执行 Affine Map。工程命名是惯例，数学审计仍需精确。

Affine Map 保持直线和平行结构，但不满足严格 Origin-preserving Superposition。

## Basis Response · 少量信息为什么决定全部变化？

任意 Vector 可写为 Basis Combination：

\[
\mathbf{x}=x_1\mathbf{e}_1+\cdots+x_n\mathbf{e}_n
\]

若 $T$ Linear：

\[
T(\mathbf{x})
=x_1T(\mathbf{e}_1)+\cdots+x_nT(\mathbf{e}_n)
\]

因此知道所有 Basis Vector 的去向，就知道任意 Input 的去向。Matrix Columns 正是这些 Basis Response。

这把 Chapter 12 的 Column View 提升为 Linear Structure 的核心理由。

## Composition · 为什么多层仍可压缩？

若：

\[
\mathbf{h}=W_1\mathbf{x},
\qquad
\mathbf{y}=W_2\mathbf{h}
\]

则：

\[
\mathbf{y}=W_2W_1\mathbf{x}
\]

两个 Linear Transformation 的 Composition 仍是 Linear。

多个 Affine Map 的 Composition 仍是 Affine：Bias 会重新组合，但不会创造阈值或弯曲。

所以只堆 `Linear/Affine` Layer，Depth 增加，Transformation 类别没有获得真正 Nonlinear Expressivity。

## Residual · Linearity 的失败留下什么证据？

观察值为 $\mathbf{y}$，Linear Prediction 为 $W\mathbf{x}$：

\[
\mathbf{r}=\mathbf{y}-W\mathbf{x}
\]

Residual 不自动说明原因。它可能来自：

- Noise；
- Missing Variable；
- Wrong Unit；
- Interaction；
- Saturation；
- Regime Shift。

研究问题是：Residual 是否随 Input、Group、Time 或 Scale 出现系统模式？

## Visualization Spine · Grid and Superposition

二维图依次显示：

1. 两个 Basis Vector；
2. 它们的 Sum；
3. Matrix 后的 Basis Response；
4. Transformed Sum 与 Sum of Transforms 重合；
5. 加 Bias 后 Origin 移动；
6. Saturating Map 下 Superposition 断裂。

图示用二维建立直觉，不声称所有高维 Transformation 可直接看见。

## Coding Lab · Test, Compose, Break

Notebook 实现三类 Function：

- `linear(x) = W @ x`；
- `affine(x) = W @ x + b`；
- `saturating(x) = tanh(W @ x)`。

对随机 $u,v,c$ 计算：

\[
\epsilon_{add}
=\lVert T(u+v)-T(u)-T(v)\rVert
\]

\[
\epsilon_{scale}
=\lVert T(cu)-cT(u)\rVert
\]

运行前预测每个 Function 的 Test Result。

Perturbation：Bias 归零、Input Scale 增大、Composition 加深、加入 Product Feature、按 Regime 分组 Residual。

## Engineering Perspective · Linear Layer 是 Baseline 与骨架

Linear/Affine Layer 的优势：

- GPU 适合 Matrix Multiplication；
- Shape 与 Composition 清晰；
- Gradient 容易传播；
- 可作为复杂系统 Baseline；
- 许多 Nonlinear Network 仍以它完成 Feature Mixing。

但工程中“可微、可扩展”不等于“表达足够”。若只堆 Affine Layer，整个 Stack 可折叠成一个 Affine Map。

本章只预告：Deep Learning 依赖 Linear Mixing 与 Nonlinear Gating 的交替，不提前教授 Activation Catalog。

## AI × Finance · Factor Model 是可检验 Baseline

\[
r_i
=\beta_{i1}f_1+\cdots+\beta_{ik}f_k+\epsilon_i
\]

Linear Factor Model 假设 Factor Effect 可以加总、缩放，并在声明的 Horizon 与 Regime 内稳定。

它的价值不只是简单：

- Exposure 可分解；
- Scenario 可组合；
- Residual 可诊断；
- 与复杂模型比较时提供 Baseline。

Failure Tests：

- Leverage × Volatility Interaction；
- Rate Threshold；
- Liquidity Saturation；
- Regime-specific Beta；
- Point-in-time Exposure Drift。

Linear Baseline 失败不是“模型没用”，而是指出哪种额外结构值得加入。

## Research Corner · 为什么复杂模型仍要研究局部 Linear Structure？

本节只提出：

1. Nonlinear Model 在小范围内何时可用 Linear Approximation 理解？
2. Linear Probe 测到 Representation 中的什么，又不能证明什么？
3. 为什么强大模型仍大量使用 Linear Projection？

候选路标聚焦 Local Linearization、Linear Probe Limitation 与 Neural Network Piecewise Structure。正文前核验 2–3 个原始来源，不提前进入 NTK、Jacobian Theory 或 Transformer 细节。

## Common Illusions

- “图像像直线”不等于满足 Superposition；
- “$y=wx+b$”严格说不一定是 Linear Transformation；
- “Fit 很好”不等于关系机制 Linear；
- “Residual 小”不等于 Boundary 外可靠；
- “多个 Linear Layer”不等于更强表达类别；
- “简单模型”不等于低价值 Baseline；
- “可解释系数”不等于因果效应；
- “局部近似 Linear”不等于全局 Linear。

## Failure Modes

### Affine-as-linear Confusion

忽略 Bias 对 Origin 的影响。

### Visual-line Test

只看图像，不测试 Additivity/Homogeneity。

### Hidden Interaction

真实 Output 依赖 Input Product 或条件组合。

### Saturation Blindness

大 Input 下比例关系失效。

### Regime Averaging

不同环境强行使用同一系数。

### Residual Neglect

只报告平均 Fit，不检查系统模式。

### Causal Overclaim

把 Linear Coefficient 当因果机制。

### Depth Illusion

堆叠 Affine Layer，却没有 Nonlinearity。

## Mental Model Upgrade

### Before

```text
Linear = straight line + simple model
```

### After

```text
Linear Transformation = additivity
                        + homogeneity
                        + origin preservation
                        + basis-determined behavior
                        + composability
                        + explicit residual boundary
```

升级完成的证据是：读者能运行 Superposition Test，区分 Linear/Affine，并用 Residual 找到失效范围。

## Learning Package Plan

### Notebook · Test, Compose, Break

比较 Linear、Affine 与 Saturating Function，运行 Additivity/Homogeneity Error，检查 Basis Reconstruction、Composition Collapse 与 Residual Pattern。

### Figure Set

1. Superposition Test；
2. Origin-preserving vs Affine Shift；
3. Basis Response Reconstruction；
4. Linear Fit and Structured Residual。

### Understanding Audit

- **Explain:** 为什么 Superposition 而非“直线”定义 Linear？
- **Predict:** Bias、Scale、Interaction 与 Saturation 怎样破坏测试？
- **Reconstruct:** 从 Basis Response 重建 Matrix Map；
- **Transfer:** 为 Sensor、Feature Layer 或 Factor Model 审计 Linearity。

### Capability Milestone

- **Explain:** distinguish Linear, Affine, and Nonlinear behavior;
- **Predict:** identify where superposition and composition fail;
- **Build:** run a reproducible linearity and residual audit;
- **Read:** challenge causal or global claims made from linear fit.

## Exercise Evidence

练习依次要求：手算 Superposition、证明 Origin Preservation、区分 Linear/Affine、从 Basis 建 Matrix、合并多层 Linear Map、运行 Residual Audit、构造 Finance Interaction，并从失败模式自然提出 Nonlinearity。

## Connection and Bridge

Chapter 12 用 Matrix 表达变化；Chapter 13 说明其中最可预测的一类变化遵守 Superposition。

但阈值、饱和、乘法交互与条件切换都会破坏这份契约。只堆 Affine Layer 仍可折叠成一个 Affine Map。

> **如果现实关系会弯曲、饱和和切换，系统怎样突破 Linear Composition 的表达边界？**

这进入 Chapter 14：**为什么非线性能够创造复杂表达？**

## Scope Boundaries

本章不完整教授：

- Vector Space Axiom 与完整证明体系；
- Determinant、Inverse、Rank、Eigenvalue；
- Taylor Series 与 Jacobian；
- Activation Function Catalog；
- SVM、Regression Theory 或统计推断；
- Transformer Projection 与 LoRA；
- Causal Inference。

这些内容只在服务“Superposition Contract 与 Linear Boundary”时准确预览。

## Definition of Done

- [ ] Opening Story 让 Linearity 成为可检验响应结构；
- [ ] Linear Transformation Audit 贯穿数学、Lab、工程与 Finance；
- [ ] Additivity 与 Homogeneity 均有直觉、公式与 Test；
- [ ] Linear 与 Affine 严格区分；
- [ ] Basis Response 连接 Matrix Column View；
- [ ] Composition Collapse 制造 Nonlinearity 需求；
- [ ] Residual 用于发现 Boundary，不被当成单一原因；
- [ ] Bridge 自然引出 Chapter 14。

## Questions for Editorial Review

1. Sensor Saturation 是否自然建立 Superposition 与 Boundary？
2. Input/Output / Additivity / Homogeneity / Origin / Basis / Composition / Residual / Boundary 是否适合作为统一 Audit？
3. Linear vs Affine 是否足够严谨又不过度纠正工程术语？
4. Basis Response 是否自然深化 Chapter 12 Column View？
5. Composition Collapse 是否讲清为什么 Depth 需要 Nonlinearity？
6. Factor Model 是否提供专业、可检验的 Finance Baseline？
7. Chapter 14 Bridge 是否自然产生弯曲、阈值与交互问题？

