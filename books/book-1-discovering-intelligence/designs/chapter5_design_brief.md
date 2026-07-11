# Chapter 5 Design Brief

**Working title:** 为什么计算能够产生智能？

**Book:** The AI Mind · Book I · Discovering Intelligence

**Author:** Codex

**Status:** Awaiting Editor-in-Chief review

**Source:** Historical Journey 05 supplies seed ideas only. The chapter will
be rewritten around the canonical Book I hidden spine and Golden Chapter
Standard.

## One Sentence

> **计算把静态表示变成可追踪的新状态；它的力量来自规则、顺序、状态与组合，而智能还需要这些计算被目标、反馈和学习组织起来。**

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
Computation (Chapter 5)
    ↓
Learning through Feedback (Chapter 6)
```

### Need Before

- Chapter 2: repeated local updates can generate global behavior;
- Chapter 3: stable contracts hide replaceable implementation detail;
- Chapter 4: models operate on representations, and computation cannot recover distinctions lost before representation.

### This Chapter

```text
input representation
  + current state
  + transformation rule
  + execution order
  + finite resources
  → trace of intermediate states
  → output representation
```

### Need After

- Chapter 6: feedback changes which computations the system performs;
- Chapters 13–14: linear and nonlinear transformations compose into neural computation;
- Chapters 18–19: computation graphs and reverse-mode differentiation;
- Part III: attention, feed-forward layers, residual streams, and autoregressive inference;
- Book III: hardware, parallelism, memory, and inference systems.

## Book I Question

**Book I 的问题：** 关系怎样逐步形成能够学习、推理与行动的智能系统？

**本章的问题：** 表示已经让关系进入机器以后，有限、机械的步骤怎样产生新的状态、结果与复杂行为？

**本章的回答：** 把输入与当前状态交给明确变换，按顺序产生可追踪中间状态；简单变换通过分支、记忆、迭代和组合，可以实现远比单步规则丰富的过程。

**下一个问题：** 如果计算规则只会忠实重复，机器怎样根据结果修改未来的计算？这进入 Chapter 6 的 Learning。

## Core Question

为什么不“理解”任务的机械步骤能够完成复杂推理？计算能力、计算资源、正确性和智能行为之间究竟是什么关系？

## Controlling Thesis

> **计算是表示之间可执行、可复现、可追踪的状态变换。复杂能力来自简单变换的组合与状态积累，但计算本身既不选择正确目标，也不会自动改进规则。**

本章拒绝两个极端：

- “机器只是在计算，所以不可能产生复杂行为”；
- “只要算力足够多，智能就会自动出现”。

前者忽略组合与状态的表达能力，后者忽略表示、算法、数据、目标、反馈和资源分配。

## Why This Chapter

Chapter 4 把世界变成机器可操作的表示，但表示仍然静止。像素不会自己识别对象，Token 不会自己形成句义，公司向量也不会自己产生判断。

系统必须执行步骤：读取、比较、选择、组合、更新与输出。若这些步骤不可复现或中间状态不可追踪，错误难以定位；若步骤固定不变，系统又无法根据经验改进。

Without computation, a represented relationship cannot **change state,
propagate influence, produce an output, or participate in a learning loop**.

## Starting Mental Model

读者可能带着以下直觉进入本章：

```text
Computation
  = arithmetic
  = CPU or GPU doing calculations
```

本章要升级为：

```text
Computation
  = representation transformation
  + state
  + control flow
  + composition
  + resource limits
  + observable trace
```

## Learning Objectives

完成本章后，读者能够：

1. 区分 arithmetic、algorithm、program、execution 与 computation；
2. 用 Input、State、Rule、Order、Resource、Trace 六个位置分析计算过程；
3. 用状态更新式表达一次计算，并解释每个符号；
4. 说明函数组合、分支、迭代和记忆怎样增加计算能力；
5. 预测改变执行顺序、精度、状态初始化或资源预算的后果；
6. 区分 deterministic computation 与 reproducible system behavior；
7. 通过一个小型状态机或流水线重建计算 Trace；
8. 把计算框架迁移到 point-in-time 投研 Pipeline；
9. 说明为什么更多 FLOPs 不自动等于更高智能；
10. 区分固定计算与通过反馈改变规则的学习。

## Opening Story · 一张谁都不知道答案的纸带

一个房间里坐着几位工作人员。每个人只收到一张操作卡：读取纸带上的符号，按条件改写一个位置，把读头向左或向右移动，再把纸带交给下一位。

没有人知道最终答案，也没有人理解整个任务。每个人只执行局部规则。

最初纸带写着一个问题。经过许多轮，纸带上出现新的中间符号；某些步骤重复，某些步骤根据当前符号分支，最后系统停在一个可读取答案上。

答案没有预先藏在某张操作卡里。它来自：

- 初始表示；
- 当前状态；
- 条件规则；
- 执行顺序；
- 中间结果被后续步骤继续读取。

故事不声称工作人员组成了智能主体。它只建立本章核心惊讶：不理解全局任务的局部执行者，仍能通过精确组合完成超出任何单步规则的过程。

类比边界：真实 CPU、GPU 和神经网络不靠人工传纸带；并行执行、数值精度和内存层级也更复杂。纸带房间只隔离 State Transition 与 Trace。

## Feynman Model · 积木工厂的六个问题

给十二岁孩子一座积木工厂。

传送带送来红色和蓝色积木。机器可以：

- 读取下一个积木；
- 根据颜色选择轨道；
- 把积木放进盒子；
- 记录盒子里已有多少块；
- 重复直到传送带结束；
- 输出装好的盒子。

孩子不需要先学 CPU。只需问六个问题：

1. **Input:** 进入机器的表示是什么？
2. **State:** 机器记住什么？
3. **Rule:** 每一步怎样改变状态？
4. **Order:** 哪一步先发生？
5. **Resource:** 时间、盒子和传送带长度有什么限制？
6. **Trace:** 怎样查看中间发生了什么？

若机器没有 State，只能处理当前积木，无法累计总数；若顺序改变，后一步可能读取错误状态；若盒子容量有限，正确算法也可能无法完成任务。

## First-Principles Spine

| Element | Core question | Failure when missing |
|---|---|---|
| Input · 输入 | 计算读取什么表示？ | 任务与数据边界不清 |
| State · 状态 | 哪些中间信息进入下一步？ | 无法积累历史或保持上下文 |
| Rule · 规则 | 当前状态怎样变换？ | 没有可执行关系 |
| Order · 顺序 | 规则何时、按什么依赖执行？ | 读取未准备或已覆盖的状态 |
| Resource · 资源 | 时间、内存、精度和带宽多少？ | 理论可行但实践无法执行 |
| Trace · 轨迹 | 如何观察中间状态与错误？ | 只有最终结果，难以验证机制 |

Trace 是本章的重要新增。相同输出可能来自不同过程；调试、审计与研究机制需要检查计算路径，而不只看答案。

## Mathematics Spine · 状态怎样一步步变化？

数学采用“积木轨迹 → 状态表 → 更新规则 → 组合函数”递进。

设第 (t) 步的状态为 (s_t)，当前输入为 (x_t)，一步更新规则为 (F)：

\[
s_{t+1}=F(s_t,x_t)
\]

执行 (T) 步后，通过读取规则 (G) 得到输出：

\[
y=G(s_T)
\]

### Composition

若计算由多个变换组成：

\[
y=f_3(f_2(f_1(x)))
\]

每个函数只完成局部变换；组合后的过程可以建立更复杂关系。这里将连接 Chapter 2 的生成观点与后续神经网络层。

### Branch

条件让同一程序根据状态选择不同变换：

\[
F(s,x)=
\begin{cases}
F_{\text{red}}(s,x), & x\text{ is red},\\
F_{\text{blue}}(s,x), & x\text{ is blue}.
\end{cases}
\]

### Iteration

重复让一次局部变换沿时间传播。它不创造输入中不存在的事实，却可以显露、聚合和重组已表示的关系。

### Resource Cost

计划只建立最小成本语言：

```text
time steps T
memory states M
numerical precision P
```

本章不教授 Big-O 推导，但要让读者知道“能算”与“在给定资源下算得出来”不是同一判断。

## Planned Visualizations

### Figure 1 · State Transition Trace

展示 Input、State、Rule 怎样形成 (s_0\rightarrow s_1\rightarrow\cdots\rightarrow s_T)，并标出 Trace 让中间状态可审计。

### Figure 2 · Composition, Branch, Memory, Iteration

四种结构怎样从简单变换构成更丰富计算，而不把图画成 CPU 架构大全。

## Engineering Spine · 一个可检查的小型状态机

Notebook 实现交易流水的状态机，而不是手写 Parser 或模拟完整 CPU。

输入事件：

```text
deposit(amount)
withdraw(amount)
fee(amount)
```

状态包含余额与处理数量。每一步返回新状态与 Trace：

```python
def step(state, event):
    ...
    return new_state, trace_entry
```

Perturbation Tests：

1. 改变事件顺序，观察余额与违规状态；
2. 忘记初始化 State；
3. 使用低精度浮点反复累计小额费用；
4. 删除 Trace，只保留最终余额；
5. 限制最多处理 (T) 个事件。

实验目标是区分：

- algorithm definition；
- one concrete execution；
- output correctness；
- process auditability；
- resource feasibility。

### AI Preview

神经网络 Forward Pass 是函数组合；Hidden State 保存上下文；Attention 按输入选择信息；Autoregressive Generation 把上一步输出放回下一步输入。

这里只预览结构，不教授 Transformer 或矩阵计算。

## AI × Finance · 投研 Pipeline 是可审计计算，不只是 Excel 结果

一份投资结论可能经过：

```text
filing and market data
  → point-in-time normalization
  → driver calculation
  → scenario update
  → valuation
  → risk and position constraints
  → decision artifact
```

最终目标价相同，不代表过程相同。若一个 Pipeline 偷看未来重述数据，另一个只使用当时可得信息，它们在回测中可能输出同一数字，却具有完全不同的可信度。

用六项框架审计：

- **Input:** 当时真正可获得的数据是什么？
- **State:** 上一版预测、仓位与假设怎样进入本轮？
- **Rule:** 每个指标怎样计算？
- **Order:** 数据清洗、标准化、预测与估值的依赖顺序是什么？
- **Resource:** 延迟、人工时间和计算预算多少？
- **Trace:** 能否从结论追溯到数据版本与中间假设？

核心迁移是 lineage：投资系统不仅要给答案，还要留下可复现的计算轨迹。

## Research Corner · 更多计算是否自动带来更强智能？

研究问题：增加计算预算时，能力提升来自更长执行、更大模型、更多数据、更好算法，还是它们之间更合理的分配？

[Hoffmann et al. (2022)](https://arxiv.org/abs/2203.15556) 在固定训练计算预算下系统比较模型规模与训练 Token 数，说明“更多参数”并不自动等于更好的计算使用；模型与数据规模需要共同配置。

理论表达能力也需要谨慎解释。[Pérez, Marinković, and Barceló (2019)](https://arxiv.org/abs/1901.03429) 研究现代神经架构的 Turing completeness，但理论上的可计算能力不等于有限精度、有限上下文、有限时间下的实际任务能力。

本章建立四个不可混淆的判断：

```text
computable in principle
  ≠ feasible under resources
  ≠ learned from available data
  ≠ reliable intelligent behavior
```

Research Corner 不展开 Scaling Laws 或复杂性理论，只训练读者看到“算力提升”时继续追问：计算了什么、用什么表示、按什么算法、接受什么反馈、付出多少资源？

## Common Illusions

- “步骤很多”不等于“推理很深”；
- “运行更快”不等于“答案更好”；
- “确定性程序”不等于“系统结果可复现”；
- “输出正确”不等于“过程可靠”；
- “理论上可计算”不等于“资源上可行”；
- “模型更大”不等于“计算预算使用更好”；
- “计算产生复杂行为”不等于“计算本身会选择目标”。

每项错觉必须配更强测试：改变顺序、限制资源、重复执行、检查 Trace、替换表示或改变反馈。

## Failure Modes

### Wrong Input Representation

计算忠实处理错误编码，得到精确但无意义的输出。

### Hidden State

系统结果依赖未记录缓存、随机种子、环境版本或外部服务，表面相同输入无法复现。

### Order Violation

后一步读取未更新、已覆盖或来自未来的数据。

### Numerical Error

有限精度、溢出与累计误差使数学上正确的规则产生错误结果。

### Resource Exhaustion

时间、内存或带宽不足，理论算法无法完成。

### No Trace

只有最终答案，无法定位错误、验证因果路径或满足审计要求。

### Fixed Objective

计算精确优化错误目标；执行能力不负责目标是否值得追求。

## Mental Model Upgrade

### Before

```text
Computation
  = arithmetic
  = faster hardware doing more calculations
```

### After

```text
Computation
  = representation transformation
  + state
  + control flow
  + composition
  + resource limits
  + observable trace
```

升级完成的证据是：读者能重建一次执行轨迹，预测顺序或资源变化的后果，并区分计算能力与学习能力。

## Learning Package Plan

### Notebook · State Transition and Trace Lab

实现交易事件状态机，记录每一步 State 与 Trace；扰动顺序、初始化、精度和资源上限。每次运行前必须预测最终输出和首个分歧步骤。

### Understanding Audit

- **Explain:** 为什么计算不是算术，也不自动等于智能？
- **Predict:** 改变执行顺序、State 或精度会怎样？
- **Reconstruct:** 从空白页重建状态更新、组合、分支与 Trace；
- **Transfer:** 把六项计算框架迁移到新 Pipeline。

### Capability Milestone

After completing the Learning Package, the learner can:

- **Explain:** describe computation as stateful representation transformation;
- **Predict:** locate the first divergence caused by order, state, or resource changes;
- **Build:** implement a small traceable state machine;
- **Read:** audit an AI or finance computation for hidden state, lineage, and feasibility.

## Exercise Evidence

练习依次要求：识别计算六要素、手算状态轨迹、比较函数组合顺序、运行前预测状态机扰动、审计 point-in-time Pipeline，并设计区分“更多计算”与“更好算法”的实验。

## Connection and Bridge

Chapter 4 决定机器能够看见和操作什么；Chapter 5 说明这些表示怎样经过规则、状态与顺序成为新表示。

但一个固定程序无论执行多少次，都不会仅因为结果不好而自行修改规则。自动售货机可以精确找零，却不会从顾客离开中发明新的定价策略。

> **如果计算只会忠实执行已有规则，那么错误结果怎样反过来改变未来的计算？**

这进入 Chapter 6：**为什么机器能够学习？**

## Scope Boundaries

本章不完整教授：

- 图灵机形式定义与可计算性证明；
- Big-O 与复杂性类别；
- CPU/GPU 微架构；
- 编译器与操作系统；
- 并发一致性模型；
- 数值分析；
- Transformer 计算细节；
- Scaling Laws。

这些主题只在服务“计算是受资源约束的可追踪状态变换”时准确预览。

## Definition of Done

- [ ] Opening Story 让局部执行与全局计算结果同时可见；
- [ ] Input / State / Rule / Order / Resource / Trace 贯穿正文；
- [ ] 数学从状态轨迹自然进入更新式、组合与分支；
- [ ] Notebook 能定位扰动后的首个分歧步骤；
- [ ] 工程部分区分算法、执行、正确性、可审计性与可行性；
- [ ] AI × Finance 使用 point-in-time lineage，而不是泛泛说“投资也是计算”；
- [ ] Research Corner 区分理论可计算、资源可行、可学习与可靠行为；
- [ ] Common Illusions 均有更强检验；
- [ ] Bridge 使 Feedback and Learning 成为下一个必要问题。

## Questions for Editorial Review

1. 纸带房间是否能展示局部规则的组合，又不误导为完整图灵机课程？
2. Input / State / Rule / Order / Resource / Trace 是否适合作为全章统一框架？
3. 状态更新、函数组合与分支是否处于 Chapter 5 合适的数学深度？
4. 交易事件状态机是否足够透明，又能产生真实的 Order / Precision / Trace 扰动？
5. Finance Pipeline 是否真正迁移计算机制并强化可复现性？
6. Research Corner 是否准确限制“更多算力等于更多智能”的主张？
