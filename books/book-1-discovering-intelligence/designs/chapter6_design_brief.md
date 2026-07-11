# Chapter 6 Design Brief

**Working title:** 为什么机器能够学习？

**Book:** The AI Mind · Book I · Discovering Intelligence

**Author:** Codex

**Status:** Awaiting Editor-in-Chief review

**Source:** Historical Journey 06 supplies seed ideas only. The chapter will
be rewritten around the canonical Book I hidden spine and Golden Chapter
Standard.

## One Sentence

> **学习不是执行更多计算，而是让经验中的反馈改变未来计算，并使系统在明确标准下产生可验证的改进。**

## Knowledge Graph · Dependency Card

```text
Relationship
  → Generation
  → Abstraction
  → Representation
  → Computation
  → Learning
  → Generalization (Chapter 7)
```

### Need Before

- Chapter 4: a model only learns from distinctions present in its representation;
- Chapter 5: computation transforms state but does not create objectives or modify its own rules merely by repetition;
- feedback matters only when it enters future computation.

### This Chapter

```text
experience
  → prediction or action
  → outcome
  → evaluation
  → credit assignment
  → update
  → retained change
  → changed future behavior
```

### Need After

- Chapter 7: changed behavior must succeed beyond remembered experience;
- Chapters 15–19: gradient, loss, optimization, chain rule, and backpropagation implement the update mechanism;
- Part III: representation learning and pretraining;
- Book III: supervised learning, self-supervision, preference learning, reinforcement learning, and continual adaptation.

## Book I Question

**Book I 的问题：** 关系怎样逐步形成能够学习、推理与行动的智能系统？

**本章的问题：** 固定计算怎样利用结果修改未来行为，而不是永远重复同一套规则？

**本章的回答：** 把经验转成可评价结果，将反馈分配给可修改部分，执行更新并保留变化；只有当后续行为按明确标准发生系统性改善时，才有学习证据。

**下一个问题：** 如果系统在已见经验上变好，它是在学习关系，还是只在记忆答案？这进入 Chapter 7 的 Generalization。

## Core Question

什么条件让一次状态变化成为“学习”，而不是记忆、缓存、随机漂移或短期适应？系统如何知道哪里需要改变，以及“变好”究竟由谁定义？

## Controlling Thesis

> **学习是反馈驱动、可保留、可评价的行为改变。经验本身不会自动教会系统；目标、信用分配与更新机制共同决定它从经验中学到什么。**

本章坚持三个边界：

- 参数变化不自动等于学习；
- 训练表现改善不自动等于未来表现改善；
- 目标分数提高不自动等于真实意图得到满足。

## Why This Chapter

Chapter 5 的状态机可以执行一百万次相同规则。若规则错误，更多执行只会稳定复制错误。

要形成学习闭环，结果必须反过来影响未来：系统需要知道发生了什么、怎样评价、哪些可修改部分应承担责任，以及变化是否保留下来。

Without learning, a computational system cannot **use experience to alter
future behavior, adapt its internal rule, or improve under a stated
criterion**.

## Starting Mental Model

读者可能带着以下直觉进入本章：

```text
Learning
  = seeing more data
  = storing more examples
  = parameters changed
```

本章要升级为：

```text
Learning
  = experience
  + evaluation
  + credit assignment
  + update
  + retention
  + evidence of future behavior change
```

## Learning Objectives

完成本章后，读者能够：

1. 区分 execution、memory、adaptation、parameter change 与 learning；
2. 用 Experience、Behavior、Outcome、Evaluation、Credit、Update、Retention 七个位置审计学习闭环；
3. 解释为什么反馈必须进入未来计算才构成学习；
4. 用参数化规则 (f_\theta) 与更新 (U) 表达最小学习系统；
5. 说明 Credit Assignment 为什么比“知道错了”更困难；
6. 预测错误标签、延迟反馈、错误目标或过大更新的后果；
7. 构建一个可扰动的一参数预测器，而不使用自动求导；
8. 区分训练数据改善与未见数据改善，为 Chapter 7 留出边界；
9. 把学习闭环迁移到 Investment Postmortem 与在线研究流程；
10. 识别 Reward Hacking、Feedback Loop 与 Non-stationarity 风险。

## Opening Story · 同一架无人机，第二次为什么不同？

一架小型无人机第一次穿过有侧风的门框时偏向左侧，撞到软垫。传感器记录轨迹，控制系统得到偏差：目标在门框中央，实际轨迹偏左。

第二次飞行可能有三种结果：

1. 系统完全不保存第一次结果，重复同一控制；
2. 系统只保存“撞过一次”的日志，却不改变控制；
3. 系统根据偏差修改控制参数，第二次提前向右补偿。

只有第三种开始形成学习证据。

但仍不能急着宣布“学会了”：风向可能已经改变，补偿可能过度，第二次成功也可能只是运气。需要重复测试，并区分已见条件与新条件。

故事建立七个问题：经历了什么？做了什么？结果怎样？谁定义好坏？哪部分负责偏差？怎样更新？变化如何保留到下一次？

类比边界：真实飞控涉及安全、动力学和复杂控制，本章不教授机器人控制。无人机只隔离“反馈如何进入未来行为”。

## Feynman Model · 会调整旋钮的投球机

给十二岁孩子一台投球机。机器只有一个可调旋钮：力度。

第一次球落在目标前方。教练不能只说“错了”，还要提供有方向的信息：短了多少。机器根据偏差把力度调高一点，下一球再试。

```text
current knob
  → throw
  → landing point
  → compare with target
  → decide knob change
  → retain new knob
```

如果教练随机打分，机器会学到噪声；如果旋钮每次改得太大，球会在目标两侧来回跳；如果改完后断电丢失旋钮位置，下一次又回到原点。

这个模型不等于神经网络，但它让 Learning 的最小闭环可见。

## First-Principles Spine

| Element | Core question | Failure when missing |
|---|---|---|
| Experience · 经验 | 系统遇到了什么输入或情境？ | 没有可学习证据 |
| Behavior · 行为 | 当前规则产生了什么预测或动作？ | 无法比较规则后果 |
| Outcome · 结果 | 环境实际返回什么？ | 只有意图，没有结果 |
| Evaluation · 评价 | 什么标准定义更好？ | 变化没有方向 |
| Credit · 归因 | 哪部分规则应为结果负责？ | 知道错了，却不知道改哪里 |
| Update · 更新 | 怎样修改可学习状态？ | 反馈不进入未来计算 |
| Retention · 保留 | 变化怎样跨经验保存？ | 每次都从头开始 |

Behavior 与 Outcome 必须区分。模型可以输出高置信预测，环境却返回相反标签；Agent 可以选择动作，奖励可能延迟许多步才出现。

## Mathematics Spine · 规则怎样因反馈改变？

数学采用“投球记录 → 参数表 → 误差方向 → 更新式”递进。

设当前可修改参数为 (\theta_t)，预测规则为：

\[
\hat{y}_t=f_{\theta_t}(x_t)
\]

环境提供目标或结果 (y_t)。评价函数给出误差信号：

\[
e_t=E(\hat{y}_t,y_t)
\]

更新规则使用经验与误差产生下一参数：

\[
\theta_{t+1}=U(\theta_t,x_t,e_t)
\]

完整闭环是：

\[
x_t
\rightarrow f_{\theta_t}
\rightarrow \hat{y}_t
\rightarrow E
\rightarrow e_t
\rightarrow U
\rightarrow \theta_{t+1}
\]

本章不定义 Gradient 或 Loss 的具体形式。这里只要求读者看见：(E) 定义怎样评价，(U) 定义反馈怎样改变未来规则。

### Learning Evidence

参数改变不是终点。需要比较更新前后行为：

\[
Q(f_{\theta_{t+1}})>Q(f_{\theta_t})
\]

其中 (Q) 是明确评价标准。Chapter 7 将追问：这个改善是否只发生在已见经验，还是能够迁移到未见输入。

## Credit Assignment · 知道错了，还要知道改哪里

投球机只有一个旋钮，归因简单。神经网络有许多参数，Agent 的结果可能来自很久以前的一串动作，投资结论也可能由数据、假设、模型和执行共同决定。

总结果为负，不说明每个步骤都应同方向修改。

```text
bad outcome
  → which decision mattered?
  → which parameter influenced that decision?
  → how much responsibility?
  → what update is justified?
```

Backpropagation、Temporal Credit Assignment 与因果实验以后会提供更具体方法。本章只建立问题。

## Engineering Spine · 一个不用 Autograd 的学习器

Notebook 使用一参数线性预测器：

\[
\hat{y}=\theta x
\]

训练样本来自近似关系 (y=2x)。更新器根据预测偏差调整 (\theta)，让读者看到参数、行为与评价如何共同变化。

```python
def predict(theta, x):
    return theta * x


def update(theta, x, target, rate):
    prediction = predict(theta, x)
    error = prediction - target
    return theta - rate * error * x
```

这里的 `error * x` 会在正文中用局部敏感性解释，但不命名为完整 Gradient Descent 推导。

Perturbation Tests：

1. learning rate 为零：有反馈，无更新；
2. learning rate 过大：更新振荡或发散；
3. 标签系统性错误：稳定学向错误关系；
4. 每轮重置参数：有更新，无 Retention；
5. 训练数据只含一个 (x)：参数可能拟合该点，却缺少 Generalization 证据；
6. 延迟或打乱反馈：Credit 错配。

每轮记录 Learning Trace：Experience、Prediction、Outcome、Error、Parameter Before、Parameter After。

## AI × Finance · Postmortem 怎样真正改变下一次决策？

投资机构会写复盘，但复盘文档存在不等于组织学习。

完整闭环：

```text
thesis and position
  → realized path and outcome
  → compare with ex-ante assumptions
  → assign error to data / model / sizing / execution
  → update checklist, prior, model, or limit
  → apply to future decision
```

用七项框架审计：

- **Experience:** 当时看到的事实与情境是什么？
- **Behavior:** 做了什么预测与仓位选择？
- **Outcome:** 基本面、价格和风险怎样发展？
- **Evaluation:** 按收益、风险调整收益、过程纪律还是预测准确度评价？
- **Credit:** 错在 Thesis、Timing、Sizing、Data 还是 Execution？
- **Update:** 修改哪条规则、参数或流程？
- **Retention:** 下一次决策是否真正调用更新后的规则？

错误目标同样危险。如果只奖励短期 P&L，系统可能学会承担隐藏尾部风险。分数提高不自动等于真实投资能力提高。

### Non-stationarity

市场参与者、制度和关系会变化。过去有效更新可能在新 Regime 中失效。学习系统不仅要更新，还要监测被学习关系是否仍稳定。

## Research Corner · 经验会教会系统什么？

研究问题：当系统从数据和反馈中改善时，它究竟学到了稳定关系、环境捷径，还是评价函数的漏洞？

本章从三类不确定性出发：

1. **Feedback quality:** 标签或奖励是否代表真实目标？
2. **Credit assignment:** 结果应归因到哪些动作或参数？
3. **Environment shift:** 更新后的关系在未来是否仍成立？

计划选择两个原始研究路标：一个展示通过反馈学习复杂行为的成功案例，一个展示错误代理目标或 Shortcut 的限制。正式正文前核验来源，不在 Design Brief 中堆叠论文。

Research Corner 不提前教授 Reinforcement Learning、Backpropagation 或 Alignment。它只建立纪律：学习到什么由经验分布、表示、目标和更新机制共同决定。

## Common Illusions

- “看过更多数据”不等于“学到了关系”；
- “参数发生变化”不等于“行为变好”；
- “训练分数提高”不等于“未来表现提高”；
- “有反馈”不等于“反馈进入了正确位置”；
- “记住失败案例”不等于“更新了决策规则”；
- “奖励更高”不等于“真实目标更好”；
- “持续在线更新”不等于“持续进步”。

每项错觉必须配更强测试：冻结时间、保留未见数据、对齐反馈、检查 Retention、构造目标漏洞或切换环境。

## Failure Modes

### No Signal

系统没有可比较结果，无法知道变化方向。

### No Credit

知道整体失败，却无法判断哪个决定或参数应改变。

### No Retention

更新没有保存，下一次计算仍使用旧规则。

### Wrong Feedback

标签、奖励或评价函数系统性偏离真实目标。

### Update Instability

更新过大、噪声过强或反馈延迟造成振荡与发散。

### Memorization

系统改善只来自保存训练案例，没有形成可迁移关系。

### Non-stationarity

环境改变，过去学习到的关系不再可靠。

### Feedback Loop

模型输出改变未来数据，使系统把自身影响误认为外部规律。

## Mental Model Upgrade

### Before

```text
Learning
  = more data
  = stored examples
  = changed parameters
```

### After

```text
Learning
  = feedback-driven retained change
  + credit assignment
  + update mechanism
  + evidence of improved future behavior
```

升级完成的证据是：读者能指出反馈怎样进入未来计算、哪里发生 Credit Assignment、变化如何保留，以及用什么证据判断行为真的改善。

## Learning Package Plan

### Notebook · Feedback-to-Update Lab

实现一参数预测器，记录每轮 Learning Trace；扰动 rate、标签、Retention、数据覆盖与反馈顺序。所有实验必须先预测参数与行为怎样变化。

### Understanding Audit

- **Explain:** 为什么经验、参数变化或记忆都不足以单独证明学习？
- **Predict:** 错误反馈、过大更新或无 Retention 会怎样？
- **Reconstruct:** 从空白页重建七项闭环与最小更新公式；
- **Transfer:** 把学习审计迁移到一个组织或 Agent Workflow。

### Capability Milestone

After completing the Learning Package, the learner can:

- **Explain:** distinguish learning from execution, memory, and random adaptation;
- **Predict:** trace how feedback quality and update choices alter future behavior;
- **Build:** implement and perturb a minimal feedback-driven learner;
- **Read:** audit an AI or finance learning loop for credit, retention, and objective mismatch.

## Exercise Evidence

练习依次要求：识别学习闭环、手算参数更新、运行前预测 Learning Trace、诊断错误反馈与无 Retention、审计投资复盘，并设计区分 Memorization 与 Learning 的测试。

## Connection and Bridge

Chapter 5 让表示经过规则成为新状态；Chapter 6 让结果反馈修改未来规则，第一次闭合：

```text
Representation
  → Computation
  → Outcome
  → Feedback
  → Update
  → Future Computation
```

但系统在训练案例上表现更好，仍可能只是记住答案。真正有用的学习必须面对没有见过的输入、条件和变化。

> **如果模型在过去经验上变好，我们怎样知道它学到的是可迁移关系，而不是一份更大的答案表？**

这进入 Chapter 7：**为什么好的模型能够举一反三？**

## Scope Boundaries

本章不完整教授：

- Loss Function 具体形式；
- Gradient 与 Gradient Descent；
- Backpropagation；
- Supervised / Unsupervised / Reinforcement Learning 完整分类；
- Bayesian updating；
- Continual Learning；
- Meta-learning；
- Reward modeling 与 Alignment。

这些主题只在服务“反馈怎样改变未来计算”时准确预览。

## Definition of Done

- [ ] Opening Story 区分日志保存、参数变化与学习证据；
- [ ] Experience / Behavior / Outcome / Evaluation / Credit / Update / Retention 贯穿正文；
- [ ] 数学从投球记录自然进入参数、评价与更新式；
- [ ] Notebook 让读者定位反馈到未来行为的完整路径；
- [ ] 工程部分不用 Autograd，并明确不提前推导 Gradient；
- [ ] AI × Finance 让 Postmortem 真正改变未来流程；
- [ ] Research Corner 讨论反馈、归因与环境变化，而非堆学习范式；
- [ ] Common Illusions 均有更强测试；
- [ ] Bridge 使 Generalization 成为下一个必要问题。

## Questions for Editorial Review

1. 无人机故事是否清楚区分日志、调整与学习证据，又不过度简化控制问题？
2. 七项 Learning Audit 是否完整但不过重？
3. (f_\theta\)、(E) 与 (U) 是否处于 Chapter 6 合适数学深度？
4. 一参数预测器是否能展示更新，又不会提前偷教 Gradient Descent？
5. Finance Postmortem 是否真正迁移 Credit、Update 与 Retention？
6. Chapter 7 的 Generalization 边界是否保留得足够清晰？
