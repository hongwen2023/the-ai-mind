# Chapter 7 Design Brief

**Working title:** 为什么好的模型能够举一反三？

**Book:** The AI Mind · Book I · Discovering Intelligence

**Author:** Codex

**Status:** Awaiting Editor-in-Chief review

**Source:** Historical Journey 07 supplies seed ideas only. The chapter will
be rewritten around the canonical Book I hidden spine and Golden Chapter
Standard.

## One Sentence

> **泛化不是在过去经验上得高分，而是在明确的新情境边界内，让学到的关系继续产生可靠结果。**

## Knowledge Graph · Dependency Card

```text
Representation
  → Computation
  → Learning
  → Generalization
  → Research Evidence (Chapter 8)
```

### Need Before

- Chapter 1: understanding includes Transfer, not recognition alone;
- Chapter 4: representation defines which similarities a model can use;
- Chapter 6: changed parameters and better training behavior do not yet prove useful Learning.

### This Chapter

```text
training experience
  → learned rule
  → held-out boundary
  → unseen experience
  → performance under stated shift
  → uncertainty and failure analysis
```

### Need After

- Chapter 8: research begins by asking which claim and evidence can distinguish competing explanations;
- Chapter 9: review the first Book I mental map through evidence;
- later ML chapters: overfitting, regularization, validation, model selection;
- Part III: scaling, in-context learning, robustness, transfer, and emergent behavior.

## Book I Question

**Book I 的问题：** 关系怎样逐步形成能够学习、推理与行动的智能系统？

**本章的问题：** 学习已经改变规则以后，怎样判断系统学到的是可迁移关系，而不是训练经验的索引？

**本章的回答：** 在更新之前定义独立测试边界，用未见经验和明确 Shift 检查行为；同时报告 Metric、Generalization Gap、不确定性与失败分组。

**下一个问题：** 如果一个结果可以由多种解释产生，我们怎样提出问题并设计证据来区分它们？这进入 Chapter 8 的 Research Mindset。

## Core Question

什么证据能区分“记住训练样本”“学到训练分布中的 Shortcut”和“学到在目标环境仍有效的关系”？所谓“新情况”究竟新在哪里？

## Controlling Thesis

> **泛化是一项带边界的经验主张：模型在未用于更新的情境中保持性能，且测试情境与未来使用之间的关系被明确说明。没有独立边界，就没有可信的泛化证据。**

本章拒绝三个过度简化：

- Test Score 不是脱离测试分布的普遍能力；
- Train–Test Gap 小不保证现实部署可靠；
- 一个新样本表现好不等于所有 Distribution Shift 都能处理。

## Why This Chapter

Chapter 6 的一参数学习器可以让训练误差下降。它也可能只记住一个点、学错标签或利用训练数据中的偶然关系。

Learning 说明过去怎样改变未来规则；Generalization 检查改变后的规则在什么未来仍有用。

Without generalization evidence, a system cannot **distinguish reusable
structure from memorization or shortcut behavior, estimate deployment risk,
or justify claims about unseen cases**.

## Starting Mental Model

```text
Generalization
  = high test accuracy
  = model works on new data
```

升级为：

```text
Generalization claim
  = training experience
  + independent holdout boundary
  + specified shift
  + relevant metric
  + uncertainty
  + failure analysis
```

## Learning Objectives

完成本章后，读者能够：

1. 区分 Memorization、Interpolation、Shortcut、Transfer 与 Generalization；
2. 使用 Training Experience、Learned Rule、Holdout Boundary、Shift、Metric、Uncertainty 审计泛化主张；
3. 解释为什么测试边界必须在模型选择与更新流程之外；
4. 计算训练误差、测试误差与 Generalization Gap；
5. 区分 in-distribution、temporal shift、group shift 与 intervention-like shift；
6. 预测模型复杂度、数据覆盖和 Leakage 对未见表现的影响；
7. 用多项式拟合实验展示 Underfitting、Interpolation 与 Overfitting；
8. 设计 Walk-forward Finance Backtest，并识别未来信息泄漏；
9. 说明为什么 Benchmark 成绩不自动代表真实世界能力；
10. 把失败案例转化为 Chapter 8 的研究问题。

## Opening Story · 老师为什么要换一道题？

老师提前发给学生一百道练习。学生 A 把答案顺序全部背下；学生 B 尝试理解题目之间的关系。

如果考试原样重复一百道题，两人都可能满分。分数无法区分记忆与理解。

老师于是改变数字、交换条件、加入一个未见组合。新题不是为了“刁难”，而是建立证据：学生能否把关系用于未见情境？

但换题也有边界。如果练习只教加法，考试突然要求微积分，失败不能简单证明学生没有学会加法。测试必须新，又必须与目标能力相关。

故事建立六个问题：训练看过什么？学到什么规则？考试怎样独立？新题新在哪里？用什么评分？一次成绩有多大不确定性？

## Feynman Model · 学会骑车，还是记住一条路？

孩子在平坦直路上学骑车。第二天换一辆车、增加小坡或出现侧风。

- 同一条路重复：接近训练经验；
- 同类道路略有变化：in-distribution variation；
- 湿滑路面或强风：larger shift；
- 要求驾驶摩托车：任务已经改变。

“能骑新路”不是二元标签。泛化主张必须说清改变了什么，以及仍假设什么不变。

类比边界：人类运动学习与机器模型机制不同。自行车只用于解释测试边界和 Shift 强度。

## First-Principles Spine · Generalization Audit

| Element | Core question | Failure when missing |
|---|---|---|
| Training Experience | 更新过程看过什么？ | 无法知道什么算未见 |
| Learned Rule | 系统可能依赖什么关系？ | 只看分数，不检查 Shortcut |
| Holdout Boundary | 哪些数据从未进入更新或选择？ | Test Leakage |
| Shift | 测试与训练在哪些维度不同？ | “新数据”含义模糊 |
| Metric | 哪种表现代表任务成功？ | 平均分隐藏关键失败 |
| Uncertainty | 结果有多稳定、样本多大？ | 把偶然波动当能力 |

Failure Analysis 横跨六项：按群组、时期、难度与扰动寻找系统性错误。

## Mathematics Spine · Gap 是证据，不是全部答案

设训练集为 (D_{\text{train}})，测试集为 (D_{\text{test}})，模型为 (f)，单样本误差为 (\ell)。

\[
\hat{R}_{\text{train}}(f)
=\frac{1}{|D_{\text{train}}|}
\sum_{(x,y)\in D_{\text{train}}}\ell(f(x),y)
\]

\[
\hat{R}_{\text{test}}(f)
=\frac{1}{|D_{\text{test}}|}
\sum_{(x,y)\in D_{\text{test}}}\ell(f(x),y)
\]

经验 Generalization Gap：

\[
\widehat{\text{gap}}
=\hat{R}_{\text{test}}(f)-\hat{R}_{\text{train}}(f)
\]

Gap 大可能表示 Overfitting；Gap 小也可能因为训练与测试共享同一 Shortcut，或两个集合都不代表部署环境。

### Distribution Boundary

训练与测试可以写成：

\[
(x,y)\sim P_{\text{train}},
\qquad
(x,y)\sim P_{\text{test}}
\]

若二者近似相同，测试主要检查 in-distribution generalization；若不同，则必须说明 Shift 类型与目标部署关系。

本章不推导 PAC Learning、VC Dimension 或 Generalization Bounds，只建立可计算评价和边界意识。

## Engineering Spine · 多项式不是为了画漂亮曲线

Notebook 从带噪声的一维关系采样少量训练点，并保留独立测试点。比较：

- degree 0/1：可能 Underfit；
- 中等 degree：捕获稳定关系；
- 很高 degree：可穿过训练点，却在中间与边界振荡。

Perturbation Tests：

1. 增加 Degree，比较 Train/Test Error；
2. 扩大训练覆盖范围；
3. 把 Test Data 用于选 Degree，制造 Validation Leakage；
4. 测试点移到训练范围之外，形成 Extrapolation；
5. 加入一个与标签偶然相关的 Shortcut Feature；
6. 多次随机采样，观察不确定性。

实验目的不是宣称复杂模型必然过拟合。现代深度网络的行为更复杂。本章只建立：独立边界、扰动、重复与失败分组。

## AI × Finance · Walk-forward 才接近真实未知

随机打乱历史时间序列会让未来信息间接进入训练。Finance 使用严格时间边界：

```text
train on information available through t
  → choose model and threshold
  → test on t+1 ... t+k
  → advance window
  → repeat without rewriting history
```

Generalization Audit：

- **Training Experience:** 当时可得财报、价格与宏观数据；
- **Learned Rule:** 因子、模型或决策规则依赖什么关系；
- **Holdout Boundary:** 未来时期未用于参数和阈值选择；
- **Shift:** Regime、流动性、政策、行业结构怎样变化；
- **Metric:** 收益、Drawdown、Turnover、Capacity 与成本；
- **Uncertainty:** 样本期、独立事件数量与置信区间。

失败案例：Survivorship Bias、Look-ahead Leakage、反复尝试后只报告最佳策略、忽略交易成本。一个漂亮 Backtest 可能只是对历史索引的记忆。

## Research Corner · 为什么能记住随机标签的模型仍会泛化？

[Zhang et al. (2016)](https://arxiv.org/abs/1611.03530) 展示大型神经网络能够拟合随机标签，同时在真实标签任务上出现良好 Generalization。这挑战了“模型容量大就必然不能泛化”的简单解释。

[Geirhos et al. (2020)](https://www.nature.com/articles/s42256-020-00257-z) 把许多部署失败统一为 Shortcut Learning：系统利用标准测试中有效、但在更具挑战条件下失效的决策规则。

[Koh et al. (2020)](https://arxiv.org/abs/2012.07421) 的 WILDS Benchmark 汇集现实 Distribution Shift，并显示标准训练方法在多种真实 Shift 下出现明显性能下降。

Research Corner 只留下三个问题：

1. 模型为什么在过参数化时仍可能泛化？
2. 测试集是否共享训练中的 Shortcut？
3. 哪种 Shift 最接近真实部署？

## Common Illusions

- “训练误差低”不等于“学到稳定关系”；
- “Test Score 高”不等于“所有新情境都可靠”；
- “Train–Test Gap 小”不等于“没有 Shortcut”；
- “数据从未见过”不等于“独立于模型选择”；
- “随机切分”不等于“适合时间与群组问题”；
- “平均准确率高”不等于“关键群组安全”；
- “更复杂模型”不必然过拟合，也不必然更好；
- “一次新样本成功”不等于可重复 Generalization。

## Failure Modes

### Memorization

训练样本表现完美，轻微变化即失败。

### Shortcut Learning

使用偶然代理关系完成 Benchmark，部署 Shift 后崩溃。

### Leakage

测试信息进入训练、特征构造、标准化或模型选择。

### Coverage Gap

训练数据没有覆盖部署所需区域或群组。

### Metric Blind Spot

平均 Metric 隐藏尾部、群组或高成本错误。

### Distribution Shift

时间、环境、制度或数据生成过程改变。

### Selection Bias

反复试验后只报告最好结果，使 Test Set 变成隐性训练集。

## Mental Model Upgrade

### Before

```text
Generalization
  = high test score
  = works on new data
```

### After

```text
Generalization claim
  = independent boundary
  + specified shift
  + relevant metric
  + uncertainty
  + failure analysis
```

升级完成的证据是：读者能说明什么真正未见、测试与部署怎样相关、模型可能利用什么 Shortcut，以及结论在哪个边界外不成立。

## Learning Package Plan

### Notebook · Fit, Hold Out, Shift

用 NumPy 多项式拟合展示训练与测试误差、复杂度、覆盖与 Extrapolation。每次改变 Degree、Split 或 Feature 前先预测 Generalization Gap 与失败区域。

### Understanding Audit

- **Explain:** 为什么 Test Score 不是脱离分布的普遍能力？
- **Predict:** Leakage、复杂度、覆盖与 Shift 怎样改变结果？
- **Reconstruct:** 从空白页重建 Generalization Audit 与 Gap；
- **Transfer:** 为一个新领域设计独立测试边界。

### Capability Milestone

After completing the Learning Package, the learner can:

- **Explain:** distinguish memorization, shortcut, and bounded generalization;
- **Predict:** identify how split design and distribution shift change evidence;
- **Build:** run a small train/holdout/shift experiment;
- **Read:** audit an AI or finance claim for leakage, coverage, and metric blind spots.

## Exercise Evidence

练习依次要求：识别测试边界、手算 Train/Test Error、运行前预测多项式扰动、构造 Shortcut、设计 Walk-forward Backtest，并把一个失败转成可区分解释的研究问题。

## Connection and Bridge

Chapter 6 让反馈改变未来规则；Chapter 7 要求用独立证据判断变化是否捕获可迁移关系。

一旦模型在某个测试上失败，至少有多种解释：表示丢失信息、训练覆盖不足、模型利用 Shortcut、评价 Metric 错误或环境已经改变。

> **面对同一个失败，我们怎样提出“为什么”，并设计证据区分这些解释？**

这进入 Chapter 8：**为什么研究总是从“为什么”开始？**

## Scope Boundaries

本章不完整教授：

- Bias–Variance 正式分解；
- PAC Learning、VC Dimension 与 Generalization Bounds；
- Cross-validation 完整方法；
- Regularization 技术清单；
- Double Descent 理论；
- Domain Adaptation 与 OOD Algorithms；
- Causal Generalization；
- Benchmark 设计大全。

这些内容只在服务“泛化是一项带测试边界的经验主张”时准确预览。

## Definition of Done

- [ ] Opening Story 同时说明新题必须独立且与目标相关；
- [ ] Generalization Audit 贯穿数学、Notebook、Finance 与 Research；
- [ ] 数学从考试记录进入 Train/Test Risk 与 Gap；
- [ ] Notebook 不把复杂模型必然等同于 Overfitting；
- [ ] Walk-forward 明确 point-in-time 与模型选择边界；
- [ ] Research Corner 连接容量、Shortcut 与现实 Shift；
- [ ] Common Illusions 均有更强测试；
- [ ] Bridge 把失败转成 Chapter 8 的研究问题。

## Questions for Editorial Review

1. 考试故事是否清楚说明独立性与任务相关性，而不把泛化简化成“换数字”？
2. 六项 Generalization Audit 是否完整且可迁移？
3. Train/Test Risk、Gap 与分布记号是否处于 Chapter 7 合适深度？
4. 多项式实验是否能展示证据边界，又避免陈旧的“复杂必过拟合”结论？
5. Walk-forward Finance 是否正确体现模型选择与未来数据隔离？
6. Research Corner 是否为 Chapter 8 提供了真正可区分的解释？
