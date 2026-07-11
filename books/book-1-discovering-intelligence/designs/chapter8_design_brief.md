# Chapter 8 Design Brief

**Working title:** 为什么研究总是从“为什么”开始？

**Book:** The AI Mind · Book I · Discovering Intelligence

**Author:** Codex

**Status:** Awaiting Editor-in-Chief review

**Source:** Historical Journey 08 supplies seed ideas only. The chapter will
be rewritten around the canonical Book I hidden spine and Golden Chapter
Standard.

## One Sentence

> **研究不是为现象寻找一个听起来合理的答案，而是设计能够区分多种解释的证据。**

## Knowledge Graph · Dependency Card

```text
Learning → Generalization Evidence → Competing Explanations
                                      ↓
                                  Research Loop
                                      ↓
                              Book I Review (Chapter 9)
```

### Need Before

- Chapter 1: understanding requires explanation, prediction, reconstruction, and transfer;
- Chapters 4–7: the same failure can come from representation, computation, feedback, shortcut, leakage, or shift;
- Chapter 7: a score is evidence under a boundary, not a complete mechanism.

### This Chapter

```text
Observation
  → Question
  → Competing Explanations
  → Discriminating Predictions
  → Intervention or Measurement
  → Evidence Update
  → Better Question
```

### Need After

- Chapter 9: review Book I as a connected evidence map rather than a summary list;
- Chapter 10: mathematics as a precise language for claims and tests;
- later books: paper reading, ablations, replication, causal reasoning, and original research.

## Book I Question

**本章的问题：** 同一个现象可能由多种机制产生，我们怎样提出可区分的解释，并让证据而不是偏好决定下一步？

**本章的回答：** 把“为什么”拆成竞争假设，为每个假设写出不同预测，设计能造成分歧的干预或测量，记录不确定性并更新解释。

**下一个问题：** 前八章的关系怎样汇成一张可以重建、质疑和继续扩展的智能地图？

## Core Question

什么让一个“为什么”成为研究问题，而不是无限追问、事后故事或立场辩论？怎样避免只寻找支持自己最喜欢解释的证据？

## Controlling Thesis

> **研究从解释分叉处开始：当多个假设都能解释已有现象时，研究者寻找它们预测不同结果的条件，并用可复现证据更新信念。**

本章区分：

- Question 不是 Topic；
- Hypothesis 不是 Guess；
- Experiment 不是 Demo；
- Evidence 不是单个支持案例；
- Revision 不是失败，而是研究输出。

## Why This Chapter

Chapter 7 展示模型部署失败可能来自多种原因。若只选一个喜欢的解释，就会把 Research 降为 Narrative。

研究需要更严格动作：列出替代解释、找出预测分歧、控制无关变化、记录结果，并让失败证据改变原判断。

Without a research loop, a learner cannot **distinguish mechanisms that
produce the same observation, design informative tests, or revise a claim
without merely replacing one story with another**.

## Starting Mental Model

```text
Research
  = read many papers
  = ask many “why” questions
  = find a novel answer
```

升级为：

```text
Research
  = competing explanations
  + discriminating prediction
  + controlled evidence
  + uncertainty
  + belief revision
```

## Learning Objectives

完成本章后，读者能够：

1. 区分 Topic、Question、Observation、Hypothesis 与 Claim；
2. 使用 Observation、Alternatives、Prediction、Intervention、Measurement、Update 审计研究；
3. 为同一现象提出至少两个可竞争解释；
4. 找出假设给出不同预测的最小条件；
5. 区分 Demonstration、Ablation、Control、Replication 与 Falsification Attempt；
6. 用证据表和简单差值表达实验结果；
7. 设计 Shortcut Dataset 的干预实验；
8. 把 Earnings Surprise 拆成可区分的金融解释；
9. 识别 Confirmation Bias、HARKing、Cherry-picking 与 Moving Goalposts；
10. 把失败实验转化为下一轮更精确问题。

## Opening Story · 两个都能解释高分的故事

一个图像模型在测试集上准确率 98%。研究团队提出两种解释：

- **H1:** 模型学会识别物体形状；
- **H2:** 模型利用背景颜色 Shortcut。

原测试集里，猫总在绿色背景，狗总在蓝色背景。H1 与 H2 都预测高分。继续收集同样结构的数据，只会让两种故事一起得分。

真正有信息的测试，是交换背景：绿色狗、蓝色猫。

- H1 预测性能大致保持；
- H2 预测性能崩溃。

研究不是先问“哪个故事更合理”，而是问：**在哪种条件下，它们会给出不同结果？**

故事边界：真实视觉模型可能同时使用形状、纹理和背景，不只二选一。二元例子用于隔离 Discriminating Evidence。

## Feynman Model · 两位侦探与一把湿伞

门口有一把湿伞。

- 侦探 A：外面下雨；
- 侦探 B：有人刚清洗过伞。

湿伞支持两种解释。继续盯着伞，不会自动解决问题。

可以检查窗外天气、地面水迹、清洁记录。好的证据不是“又找到一个湿的地方”，而是两种解释对该证据预测不同。

侦探类比不意味着研究总有唯一真相。它只强调：解释必须承担预测后果。

## First-Principles Spine · Research Audit Framework

| Element | Core question | Failure when missing |
|---|---|---|
| Observation | 发生了什么，测量边界是什么？ | 把解释混进事实 |
| Alternatives | 还有哪些机制能产生同一现象？ | 只验证首选故事 |
| Prediction | 每个解释在新条件下预测什么？ | 假设不可区分 |
| Intervention | 怎样主动改变关键条件？ | 只有相关观察 |
| Measurement | 用什么 Metric、Control 与不确定性？ | 结果不可比较 |
| Update | 哪种结果会改变原判断？ | 假设免疫于证据 |

Reproducibility 横跨六项：别人能否重建数据、条件、代码与分析选择？

## Mathematics Spine · 证据必须改变相对解释力

用假设表先于公式：

| Condition | H1 Shape | H2 Background |
|---|---:|---:|
| Original background | high | high |
| Swapped background | high | low |

原条件无法区分，交换条件产生预测分歧。

最小实验差值：

\[
\Delta = M_{\text{intervention}}-M_{\text{control}}
\]

其中 (M) 是同一 Metric。若交换背景后 (\Delta\) 大幅为负，更支持 Shortcut 解释，但仍需重复、置信区间与其他混杂检查。

可以用条件证据语言：

\[
P(E\mid H_1)\quad\text{versus}\quad P(E\mid H_2)
\]

本章不推导 Bayes 定理或统计检验，只建立：证据的价值来自它在竞争解释下出现概率不同。

## Engineering Spine · Ablation 不是随便删东西

Notebook 构造 Shape 与 Background 两个特征：训练中背景与标签完美相关，形状也相关。比较两个规则：

- Shape Rule；
- Background Rule。

两者在原 Test 上同分，在 Background Swap 后分离。

Perturbation Tests：

1. 交换背景；
2. 破坏形状；
3. 同时加入噪声；
4. 改变 Metric；
5. 重复不同随机种子；
6. 只报告支持首选解释的条件，观察 Cherry-picking。

研究 Trace 记录 Question、Hypotheses、Pre-registered Prediction、Intervention、Metric、Result、Revision。

## AI × Finance · Earnings Miss 到底说明什么？

公司利润低于预期，可能来自：

- H1：需求走弱；
- H2：汇率折算；
- H3：渠道去库存；
- H4：一次性投入提前；
- H5：会计确认时点变化。

总利润数字不能区分。每个解释必须承担不同预测：订单、价格、库存、地区收入、现金流和下一季指引会怎样？

研究设计：

```text
Observation: margin miss
  → alternatives
  → discriminating indicators
  → management / channel / filing evidence
  → update thesis and position
```

避免事后叙事：在下一份数据出现前写出每个假设的预测与失效条件。

## Research Corner · 为什么 Ablation 仍可能误导？

删除模块后性能下降，可能因为模块承担目标机制，也可能因为干预破坏分布、尺度或优化稳定性。Ablation 是证据，不自动是因果解释。

研究问题限定为：

1. 哪些 Control 能排除“只是破坏系统”的解释？
2. Replication 复现结果，是否也复现机制？
3. Negative Result 怎样缩小假设空间？

候选阅读路标在正文前核验原始来源，限制 2–3 项，不把本章变成科学哲学史。

## Common Illusions

- “问了为什么”不等于问题可研究；
- “找到支持案例”不等于排除替代解释；
- “相关性稳定”不等于机制正确；
- “Ablation 降分”不等于模块是唯一原因；
- “实验失败”不等于没有研究产出；
- “论文复现”不等于理论解释被证明；
- “更多论文引用”不等于证据更强；
- “新方法胜出”不等于问题被解决。

## Failure Modes

### One-Hypothesis Research

只设计能支持首选解释的实验。

### Confirmation Bias

选择性寻找、解释和报告支持证据。

### HARKing

看到结果后把事后故事写成事前假设。

### Moving Goalposts

每当证据反驳，就修改成功标准保护主张。

### Confounded Intervention

同时改变多个条件，无法知道哪一项造成结果。

### Metric Substitution

使用易测代理取代真正问题，并忘记代理边界。

### Irreproducible Trace

缺少数据版本、随机种子、代码和分析选择。

## Mental Model Upgrade

### Before

```text
Research = ask why + read papers + find an answer
```

### After

```text
Research = competing explanations
           + discriminating predictions
           + controlled evidence
           + uncertainty
           + belief revision
```

升级完成的证据是：读者能写出会让自己改变判断的结果，而不只是收集支持材料。

## Learning Package Plan

### Notebook · Competing Explanations Lab

构造 Shape/Background Shortcut 数据，运行 Control 与 Intervention，比较两套规则，并记录预注册预测与 Evidence Update。

### Understanding Audit

- **Explain:** 为什么一个合理解释仍不足够？
- **Predict:** 两个假设在哪种干预下分离？
- **Reconstruct:** 从空白页重建 Research Audit；
- **Transfer:** 把一个 AI 或 Finance 现象改写成竞争假设与实验。

### Capability Milestone

- **Explain:** distinguish observation, hypothesis, and evidence;
- **Predict:** design a condition where explanations diverge;
- **Build:** run a controlled intervention with a Research Trace;
- **Read:** audit a paper or investment thesis for controls and alternative explanations.

## Exercise Evidence

练习依次要求：分离事实与解释、生成竞争假设、填写预测表、设计 Control/Ablation、运行 Shortcut 实验、重构 Earnings Miss 假设树，并把 Negative Result 写成下一问题。

## Connection and Bridge

Chapter 7 说明能力主张需要边界；Chapter 8 说明机制主张需要区分解释的证据。

完成前八章后，读者已经拥有关系、生成、抽象、表示、计算、学习、泛化与研究证据。下一步不是加入新概念，而是检查这张地图能否从空白页重建，并发现仍缺少的连接。

> **如果知识是一张关系地图，我们能否不看原文，重新画出智能系统的第一张完整地图？**

这进入 Chapter 9：**第一幕复盘——构建第一张 AI 思维地图。**

## Scope Boundaries

本章不完整教授：

- 科学哲学史；
- Bayes 定理与统计检验；
- 因果推断完整框架；
- 实验设计与 A/B Testing 全课程；
- 论文写作规范；
- Mechanistic Interpretability 方法大全；
- Meta-science 与 Publication Bias 文献。

这些内容只在服务“设计区分解释的证据”时准确预览。

## Definition of Done

- [ ] Opening Story 让两个解释在原分布同分、干预后分离；
- [ ] Research Audit Framework 贯穿 AI、Finance 与 Notebook；
- [ ] 数学从预测表进入 Intervention Difference；
- [ ] Notebook 要求事前预测并保留 Research Trace；
- [ ] Finance 使用可证伪指标而非事后故事；
- [ ] Research Corner 明确 Ablation 的解释边界；
- [ ] Common Illusions 均有更强检验；
- [ ] Bridge 使 Chapter 9 成为地图重建而非普通总结。

## Questions for Editorial Review

1. Shape/Background 故事是否足够透明，又不会把真实模型机制简化成二选一？
2. Observation / Alternatives / Prediction / Intervention / Measurement / Update 是否适合作为统一 Research Audit？
3. (\Delta) 与 (P(E\mid H)) 是否处于 Chapter 8 合适数学深度？
4. Shortcut Notebook 是否真正区分解释，而不只是演示分布偏移？
5. Earnings Miss 是否提供专业且可迁移的 Finance Research Loop？
6. Bridge 是否让 Chapter 9 成为 Understanding Audit 的书级版本？
