# Chapter 10 Design Brief

**Working title:** 为什么数学是智能的语言？

**Book:** The AI Mind · Book I · Discovering Intelligence

**Author:** Codex

**Status:** Awaiting Editor-in-Chief review

**Role in Book I:** Close Act I by translating its relationship map into
precise, computable, and testable claims. This is not a mathematics survey.

## One Sentence

> **数学不是把世界变难，而是让关系承担明确、可计算、可反驳的含义。**

## Knowledge Graph · Dependency Card

```text
Relationship Map
  → ambiguity becomes visible
  → Mathematical Language
      ├─ precise objects
      ├─ explicit relations
      ├─ valid operations
      ├─ checkable consequences
      └─ stated boundaries
  → Vector (Chapter 11)
```

### Need Before

- Chapter 1：理解意味着能够解释、预测、重建与迁移；
- Chapter 3：抽象是任务相关契约；
- Chapter 4：表示决定可见关系与可用操作；
- Chapter 9：自然语言 Edge 仍缺少数量、方向和检验规则。

### This Chapter

```text
vague claim
  → define objects
  → specify relation
  → choose representation and operation
  → derive consequence
  → compare with evidence
  → revise assumptions or boundary
```

### Need After

- Chapter 11：一个数量不足以描述多属性对象时，为什么需要 Vector；
- Chapters 12–19：Matrix、Gradient、Loss、Optimization 与 Backprop；
- 后续 Books：Probability、Attention、Scaling 与系统性能分析。

## Book I Question

**本章的问题：** 当“相似”“影响”“增加”“误差”和“证据”含义模糊时，怎样让关系变得可计算、可比较、可检验？

**本章的回答：** 定义对象与单位，明确关系、操作、假设和边界，从表达式推导预测，再让观察结果检验整套翻译。

**下一个问题：** 如果一个对象同时拥有许多相关属性，一个数字为什么不够？

## Core Question

数学为什么不是学习 AI 前必须跨过的障碍，而是智能系统用来压缩关系、执行推理并暴露错误的一种语言？形式化何时澄清问题，何时只是让错误显得精确？

## Controlling Thesis

> **数学的力量不在符号更多，而在它迫使我们声明对象、关系、假设、操作与边界，并让这些声明产生可以被计算和检验的后果。**

本章区分：

- Symbol 不是 Understanding；
- Formula 不是 Truth；
- Precision 不是 Accuracy；
- Calculation 不是 Reasoning 的全部；
- Formalization 不是删除现实边界。

## Why This Chapter

Chapter 9 的地图可以写：

```text
Representation affects Computation.
Learning improves behavior.
Two companies are similar.
The model is uncertain.
```

每句话都合理，却仍然隐藏关键问题：

- “affects” 的方向和幅度是什么？
- “improves” 用哪个 Metric？
- “similar” 基于哪些属性与尺度？
- “uncertain” 是数据噪声、模型差异还是主观保留？

数学不是在故事后面加公式。它是一套翻译纪律，让模糊关系承担可检查的含义。

Without mathematical language, a learner cannot **state a model precisely,
derive what it predicts, detect an inconsistent assumption, or distinguish a
calculation error from a modeling error**.

## Starting Mental Model

```text
Mathematics
  = formulas
  = difficult calculation
  = prerequisite to memorize before AI
```

升级为：

```text
Mathematics
  = representation of relationships
  + explicit assumptions
  + valid operations
  + derived consequences
  + evidence check
```

## Learning Objectives

完成本章后，读者能够：

1. 解释数学为何是关系语言而不只是计算工具；
2. 使用 Object、Relation、Operation、Assumption、Quantity、Test、Boundary 审计形式化；
3. 将模糊自然语言主张翻译成变量、单位和关系；
4. 区分 Definition、Assumption、Derivation 与 Observation；
5. 解释一个公式怎样压缩一族关系；
6. 通过 Units、Limiting Case 与 Perturbation 检查表达式；
7. 识别 Precise but Wrong、Proxy Substitution 与 Undefined Symbol；
8. 将 AI 系统主张转换成可执行 Test；
9. 将“便宜”“优质”“相似”转换成有边界的金融模型；
10. 说明为什么多属性对象自然要求 Vector。

## Opening Story · “再近一点”到底是多少？

两支团队远程操控一台深海机器人。视频信号延迟，机械臂正在接近一条脆弱管线。

操作员说：

> “再近一点，速度慢一些。”

工程师必须立即追问：

- 近多少厘米？
- “速度”是机械臂末端还是关节转速？
- 哪个坐标系？
- 延迟多久？
- 安全边界是多少？
- 传感器误差多大？

自然语言表达了意图，却不足以安全执行。团队把任务写成对象、位置、速度、方向、单位、约束和停止条件。

数学没有替代现实判断。它把隐藏假设暴露出来，使不同人和机器能够执行同一关系，并在后果不符时定位错误。

故事边界：精确指令仍可能建立在错误传感器或错误模型上。数学保证表达明确，不保证表达真实。

## Feynman Model · 食谱为什么需要单位？

一张食谱写：

> 加一些面粉，少量水，烤到差不多。

熟练厨师可能凭经验成功，新手和机器却无法稳定重建。

加入克、毫升、温度和时间后，食谱变得可执行、可比较、可调整。

```text
ingredient → object
amount     → quantity + unit
mix        → operation
temperature/time → condition
taste/texture     → test
oven type         → boundary
```

但“200°C 30 分钟”也不是永恒真理：烤箱、海拔、模具和目标口感会改变结果。数学食谱是带边界的模型。

## First-Principles Spine · Mathematical Translation Audit

| Element | 核心问题 | 缺失时的失败 |
|---|---|---|
| Object | 我们在描述什么？ | 符号无对象 |
| Relation | 对象怎样关联？ | 只有变量列表 |
| Operation | 允许怎样变换？ | 计算无语义 |
| Assumption | 哪些条件暂时视为成立？ | 推导边界隐藏 |
| Quantity | 怎样测量，单位是什么？ | 比较不成立 |
| Test | 哪种观察支持或反驳？ | 公式免疫于证据 |
| Boundary | 何时不再适用？ | 精确地过度推广 |

翻译顺序：

```text
meaning
  → objects and units
  → relation
  → symbols
  → operation
  → consequence
  → test and boundary
```

符号不是第一步。若不知道符号代表什么，公式只是在压缩困惑。

## Fuzzy Claim to Checkable Model

从一句话开始：

> 广告投入增加，销售也会增加。

第一轮翻译：

- $x$：广告投入，单位万元；
- $y$：销售额，单位万元；
- 时间窗口：同一季度；
- 其他条件：暂时固定；
- 关系：在研究范围内近似线性。

\[
y=wx+b
\]

这里：

- $w$ 表示单位投入对应的预测销售变化；
- $b$ 表示模型中的基准项；
- 线性是 Assumption，不是数据自动证明的真理。

模型产生可检验后果：

\[
\Delta y=w\Delta x
\]

若投入增加 $\Delta x$，销售预测改变 $w\Delta x$。真实观察不符时，可能是参数错误、非线性、时间延迟、混杂变量或边界外使用。

## Mathematics Spine · 四种数学动作

本章围绕四种动作，而非学科目录：

### Represent

用变量、集合、图或向量保存任务所需关系。

### Transform

用操作把一个状态变成另一个状态。

\[
y=f(x)
\]

### Compare

定义差异、顺序、距离或概率。

\[
\text{error}=\text{prediction}-\text{observation}
\]

### Infer

从 Assumption 与 Observation 推导 Consequence，并检查是否成立。

数学不只给答案。它保存一条可复查的推理 Trace。

## Three Fast Checks Before Trusting a Formula

### Units

等式两边单位是否一致？若 $w$ 的单位无法让 $wx$ 变成销售额，模型翻译有问题。

### Limiting Case

当输入为零、极大或极小时，公式是否产生合理后果？

### Perturbation

输入轻微变化时，输出方向和幅度是否符合主张？

这些检查不能证明模型正确，但能快速暴露许多不一致。

## Engineering Spine · 从模糊需求到 Executable Contract

需求：

> “相似用户应该得到相似推荐。”

工程团队必须定义：

1. 用户对象包含哪些 Feature？
2. Similarity 使用什么表示和尺度？
3. Recommendation Difference 怎样测量？
4. 哪些敏感属性不应产生不公平差异？
5. 多大的变化算违反 Contract？

Lab 先写自然语言 Contract，再写最小函数与 Test：

```python
def distance(user_a, user_b):
    ...


def recommendation_gap(rec_a, rec_b):
    ...
```

Perturbation Tests 改变 Feature Scale、Unit、Missing Value、Threshold 与 Representation。目标不是实现推荐系统，而是检查形式化是否忠于原问题。

## AI × Finance · “便宜且优质”不是模型

投资者说一家公司“便宜且优质”。自然语言有方向感，却不足以比较公司、复现决策或检验历史表现。

翻译可能定义：

- Value：Free-cash-flow yield、EV/EBIT 或相对历史估值；
- Quality：ROIC、Margin Stability、Balance-sheet Risk；
- Growth：Revenue、Unit Economics、Reinvestment Runway；
- Boundary：行业、会计口径、周期阶段与数据可得时间。

形式化后仍有选择：

\[
\text{score}=w_vV+w_qQ+w_gG
\]

权重、标准化与数据窗口都是 Assumption。Score 精确，不代表公司价值被完整表示。

Finance Audit：

```text
investment phrase
  → variables and units
  → relationship and weights
  → point-in-time data
  → decision rule
  → out-of-sample test
  → boundary and revision
```

真正价值在于暴露争议：两位分析师不同意的是数据、定义、权重、关系，还是边界？

## Research Corner · 形式化什么时候会误导？

研究问题限定为：

1. 一个精确 Proxy 是否替代了真正目标？
2. 更复杂公式是否只隐藏更多 Assumption？
3. 同一自然语言概念能否有多个合理形式化？
4. Metric 成为目标后，系统行为会怎样改变？

候选路标聚焦模型边界、Measurement 与 Goodhart-style failure。正文前核验原始来源，限制 2–3 项，不把本章变成哲学或统计学综述。

## Common Illusions

- “有公式”不等于有理解；
- “数字更精确”不等于模型更准确；
- “单位一致”不等于关系真实；
- “能计算”不等于值得计算；
- “拟合良好”不等于 Assumption 正确；
- “符号复杂”不等于思想深刻；
- “一个 Score”不等于对象只有一个维度；
- “数学客观”不等于建模选择中没有价值判断。

## Failure Modes

### Undefined Object

符号没有清楚对应现实对象。

### Unit Mismatch

看似可算，量纲不一致。

### Precise but Wrong

表达非常精确，假设或数据却错误。

### Proxy Substitution

用易测 Metric 替代真正目标，并忘记边界。

### Hidden Assumption

推导依赖条件没有声明。

### Operation Without Meaning

数学操作合法，现实语义不成立。

### Single-number Collapse

把多维对象过早压缩成一个 Score。

### Boundary Erasure

把局部有效关系推广到所有情境。

## Mental Model Upgrade

### Before

```text
Mathematics = formulas to memorize before doing AI
```

### After

```text
Mathematics = precise objects
              + explicit relationships
              + valid operations
              + derived consequences
              + testable boundaries
```

升级完成的证据是：读者能从现实主张建立形式化，也能从公式返回现实含义、Assumption 与 Failure Boundary。

## Learning Package Plan

### Workbook · Meaning Before Symbols

每个任务分两列：

1. 自然语言中的 Object、Relation 与 Boundary；
2. 对应 Symbol、Unit、Operation、Prediction 与 Test。

### Notebook · Translate, Compute, Break

用广告投入或简单评分模型完成：

1. 声明变量与单位；
2. 计算预测；
3. 检查 Units 与 Limiting Case；
4. 改变 Scale、Proxy 或 Boundary；
5. 记录 Mathematical Translation Audit。

### Understanding Audit

- **Explain:** 数学为何是关系语言，而非符号集合？
- **Predict:** 一个 Assumption 或 Unit 改变后，结论怎样变化？
- **Reconstruct:** 从自然语言重建公式，也从公式恢复含义；
- **Transfer:** 将同一翻译纪律用于 AI、物理或 Finance。

### Capability Milestone

- **Explain:** distinguish formula, assumption, derivation, and evidence;
- **Predict:** audit consequences with units, limits, and perturbations;
- **Build:** translate a fuzzy claim into an executable contract;
- **Read:** locate hidden assumptions and proxy substitutions in a model.

## Exercise Evidence

练习依次要求：识别对象与关系、补单位、区分 Definition/Assumption/Observation、翻译模糊主张、反向解释公式、执行三个快速检查、审计 Finance Score，并指出何时需要 Vector。

## Connection and Bridge

Chapter 9 让关系地图可见；Chapter 10 让每条关系承担更精确含义。

但当我们描述一家公司、一张图片或一个 Token 时，一个数字无法同时保存所有相关属性。若强行压成单个 Score，许多关系会在计算前消失。

> **当一个对象同时拥有多个可以独立变化、又彼此相关的属性时，我们需要怎样的数学对象？**

这进入 Chapter 11：**为什么向量比数字更适合描述世界？**

## Scope Boundaries

本章不：

- 按 Linear Algebra、Calculus、Probability 罗列课程；
- 进行大量代数技巧训练；
- 推导统计检验或因果推断；
- 声称数学模型等于现实；
- 把符号密度当数学深度；
- 提前完整教授 Vector、Matrix 或 Gradient。

所有内容只服务一个目标：让关系变得精确、可计算、可比较、可检验，同时保留现实边界。

## Definition of Done

- [ ] Opening Story 让精确关系成为安全执行的必要条件；
- [ ] Mathematical Translation Audit 贯穿 AI、Finance 与 Lab；
- [ ] 正文始终 Meaning Before Symbols；
- [ ] 公式只服务关系、预测与边界；
- [ ] Units、Limiting Case、Perturbation 形成快速检查；
- [ ] Finance 形式化暴露定义、权重与 Point-in-time 边界；
- [ ] Common Illusions 区分 Precision 与 Truth；
- [ ] Bridge 自然制造对 Vector 的需求。

## Questions for Editorial Review

1. 本章是否解释数学的必要性，而不是提前教授数学目录？
2. 深海机器人 Opening 是否使 Precision、Unit、Coordinate 与 Boundary 自然出现？
3. Object / Relation / Operation / Assumption / Quantity / Test / Boundary 是否适合作为统一 Audit？
4. $y=wx+b$ 是否提供足够形式化，又不会抢占后续章节？
5. Units / Limiting Case / Perturbation 是否是初学者合适的快速检查？
6. Finance Score 是否暴露建模选择，而不是把 Score 当真值？
7. Chapter 11 Bridge 是否让 Vector 成为多属性表示的自然答案？

