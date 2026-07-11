# Chapter 17: 为什么优化能够让模型越来越好？

> Book I · Discovering Intelligence  
> Act II · 数学如何变成智能

## Learning Objectives

完成本章后，你应该能够回答：

- 优化（Optimization）在机器学习中到底解决什么问题。
- 为什么有了 Loss 和 Gradient，还需要 Optimizer。
- 学习率（Learning Rate）为什么如此重要。
- Gradient Descent、SGD、Momentum、Adam 的直觉差异是什么。
- 为什么优化不是简单地“往下降”。
- 为什么真实 AI 训练会遇到震荡、发散、鞍点和过拟合。
- 为什么投资组合优化与模型训练共享同一类思维。

## Opening Story: 走得太慢，永远到不了；走得太快，会摔下山

上一章我们说，Loss 像地形图上的海拔。

Chapter 15 告诉我们，Gradient 像脚下最陡的坡度。

现在你站在山坡上，知道哪边下坡最快。

问题来了：

> 每一步应该走多远？

如果你每次只移动一厘米，方向可能是对的，但你可能一整晚都走不到山谷。

如果你每次迈出十米，速度很快，但很可能一步跨过低谷，甚至摔到更糟糕的位置。

知道方向，不等于会走路。

优化要解决的正是这个问题：

> 在一个复杂的 Loss Landscape 里，如何一步一步修改参数，让模型变得更好？

## The One Sentence

> Optimization 是把梯度提供的方向，变成一系列稳定、有效、可持续的参数更新。

## Why Before What

为什么不能直接用梯度？

因为梯度只回答一个局部问题：

```text
如果我站在这里，哪个方向让 Loss 上升最快？
```

训练时我们反方向走，但梯度没有告诉我们：

- 走多大一步；
- 是否要记住过去的方向；
- 不同参数是否应该用不同步长；
- 噪声很大时是否要平滑；
- 走错了是否要减速；
- 平坦区域是否要加速。

这些都是 Optimizer 要处理的问题。

所以优化不是梯度本身，而是使用梯度的策略。

## Feynman Explanation

想象你在雾里骑自行车下山。

你能感觉到坡度。坡度就是梯度。

但你还需要决定：

- 刹车还是加速；
- 转弯要不要慢一点；
- 路面颠簸时要不要稳住方向；
- 连续下坡时要不要利用惯性；
- 突然变陡时要不要减小步伐。

如果只知道坡度，不会控制速度，你仍然可能摔倒。

Optimizer 就像骑车策略。

它不改变目标：你仍然想下山。

但它决定你如何安全、高效地走向更低的地方。

## Historical Background

优化不是深度学习发明的。数学、物理、工程、经济学、金融学都长期研究优化。

但深度学习让优化问题变得特别困难：

- 参数极多；
- Loss landscape 高维；
- 数据有噪声；
- 计算成本巨大；
- 梯度可能不稳定；
- 目标函数不一定完美代表真实目标。

早期机器学习常用较简单的 Gradient Descent 或 Stochastic Gradient Descent。

后来，人们加入 Momentum，让优化器记住过去的方向。

再后来，AdaGrad、RMSProp、Adam、AdamW 等方法出现，让不同参数可以自适应调整更新幅度。

现代大模型训练中，优化器选择、学习率调度、warmup、weight decay、gradient clipping 都可能决定一次训练是否成功。

优化不是附属品。它是让模型真正学起来的工程核心。

## First Principles

训练循环可以写成：

```text
prediction = model(x)
loss = loss_fn(prediction, target)
gradient = d loss / d parameters
parameters = optimizer(parameters, gradient)
```

前三步回答：

- 模型现在怎么预测？
- 预测有多差？
- 每个参数该往哪里改？

最后一步才是优化：

> 如何根据梯度更新参数？

最简单的更新规则是 Gradient Descent：

```text
theta_new = theta_old - learning_rate * gradient
```

其中 `learning_rate` 决定每一步走多大。

这一个小数字，常常决定训练是成功、缓慢、震荡还是彻底发散。

## Intuition: Learning Rate 是步幅

学习率太小：

```text
Loss: 10.0 → 9.99 → 9.98 → 9.97
```

方向对，但太慢。

学习率太大：

```text
Loss: 10.0 → 8.0 → 12.0 → 30.0
```

一开始看似有效，随后越走越糟。

合适的学习率：

```text
Loss: 10.0 → 6.5 → 4.1 → 2.3 → 1.4
```

既不拖沓，也不乱跳。

这就是优化中最朴素的直觉：

> 方向重要，步幅同样重要。

## Mathematics: Gradient Descent

假设我们要最小化：

```text
L(w) = (w - 3)^2
```

梯度是：

```text
dL/dw = 2(w - 3)
```

更新规则：

```text
w = w - lr * 2(w - 3)
```

如果 `w = 0`，`lr = 0.1`：

```text
gradient = 2(0 - 3) = -6
w_new = 0 - 0.1 * (-6) = 0.6
```

`w` 从 0 走向 3。

下一步：

```text
gradient = 2(0.6 - 3) = -4.8
w_new = 0.6 - 0.1 * (-4.8) = 1.08
```

越接近最小值，梯度越小，更新也越小。

这正是梯度下降自然减速的原因。

## Visualization: 低谷、震荡与发散

想象一个 U 型山谷：

```text
Loss
  ▲
  │        \      /
  │         \    /
  │          \  /
  │           \/
  └────────────────► parameter
```

学习率合适时：

```text
left → center → lower → minimum
```

学习率太大时：

```text
left → right wall → left wall → right wall
```

模型在低谷两侧来回震荡。

更糟糕时，步子大到越走越高，训练发散。

所以优化不是“有梯度就行”，而是要控制更新动态。

## From GD to SGD

Full-batch Gradient Descent 每次用全部数据计算梯度。

这很稳定，但在大数据上太贵。

Stochastic Gradient Descent（SGD）每次只用一小批样本估计梯度。

它的优点：

- 计算便宜；
- 更新频繁；
- 梯度噪声有时帮助逃离坏区域。

它的缺点：

- 更新方向有噪声；
- Loss 曲线更抖；
- 需要更仔细调学习率。

深度学习中的训练通常使用 mini-batch SGD 或它的变体。

这也是为什么训练日志里的 Loss 不一定平滑下降。它常常是带噪声地下降。

## Momentum: 让优化器记住方向

如果你推一个小球下山，它不会每一步都重新开始。

它有惯性。

Momentum 的直觉就是：

> 如果过去几步都往同一个方向走，那就更相信这个方向。

普通 SGD 只看当前梯度。

Momentum 会把过去梯度也纳入考虑：

```text
velocity = beta * velocity + gradient
theta = theta - lr * velocity
```

这样可以减少来回震荡，并在稳定方向上加速。

## Adam: 给每个参数不同的步幅

Adam 是现代深度学习中非常常用的优化器。

它结合了两个思想：

1. Momentum：记住梯度的一阶趋势。
2. Adaptive scaling：根据梯度历史大小调整每个参数的步幅。

直觉上，Adam 会问：

> 这个参数过去的梯度大不大？方向稳不稳定？我应该给它多大的更新？

所以 Adam 往往比普通 SGD 更容易上手，尤其是在深度网络和 Transformer 训练中。

但 Adam 不是魔法。它也需要学习率、weight decay、warmup 等配合。

现代 LLM 训练常用 AdamW。AdamW 把 weight decay 的处理方式做得更合理，是很多大模型训练的默认选择。

## Coding Lab: 手写优化过程

```python
w = 0.0
lr = 0.1

for step in range(20):
    loss = (w - 3) ** 2
    grad = 2 * (w - 3)
    w = w - lr * grad
    print(step, round(w, 4), round(loss, 4))
```

你可以尝试把 `lr` 改成：

```python
0.01
0.1
0.9
1.1
```

观察训练变慢、变快、震荡或发散。

这个小实验比背公式重要。

优化首先是一种动态系统直觉。

## PyTorch Lab

下面是一个最小 PyTorch 优化循环：

```python
import torch

w = torch.tensor(0.0, requires_grad=True)
optimizer = torch.optim.SGD([w], lr=0.1)

for step in range(20):
    optimizer.zero_grad()
    loss = (w - 3) ** 2
    loss.backward()
    optimizer.step()
    print(step, w.item(), loss.item())
```

这里有四个关键动作：

```text
zero_grad
  ↓
loss
  ↓
backward
  ↓
step
```

`optimizer.step()` 才是真正修改参数的地方。

`loss.backward()` 只计算梯度。

这两个动作不要混淆。

## Engineering Perspective

真实训练中，优化器不仅仅是一个公式。

工程师需要考虑：

- learning rate；
- batch size；
- warmup；
- decay schedule；
- weight decay；
- gradient clipping；
- mixed precision；
- distributed training；
- checkpoint restart；
- optimizer state memory。

例如 Adam 需要保存额外状态，因此内存消耗比 SGD 更高。

在大模型训练中，优化器状态可能占用非常大的显存。ZeRO、FSDP 等分布式训练技术，一部分目的就是管理这些状态。

所以优化不是一个抽象数学话题。它直接影响训练成本、稳定性和可扩展性。

## Failure Modes

### Failure 1: Learning rate too high

Loss 可能震荡或发散。

### Failure 2: Learning rate too low

训练非常慢，看起来像没有学习。

### Failure 3: Bad schedule

一开始学习率太大，模型不稳定；后期学习率太大，模型难以收敛。

### Failure 4: Sharp minima

优化器可能找到训练 Loss 很低但泛化不好的区域。

### Failure 5: Optimizing the wrong objective

如果 Loss 本身不代表真实目标，优化器越强，错误越快。

### Failure 6: Engineering instability

混合精度、梯度爆炸、分布式同步错误，都可能让优化过程失败。

## AI x Finance

金融里也有优化。

投资组合优化常常问：

> 如何分配权重，让收益、风险、回撤和约束达到某种平衡？

这和模型优化很像：

```text
parameters  -> portfolio weights
loss        -> risk / tracking error / negative utility
gradient    -> marginal effect of changing weights
optimizer   -> rebalancing rule
```

但金融优化比标准机器学习更危险。

原因是市场目标不稳定：

- 历史协方差未来可能失效；
- 交易成本会改变最优解；
- 风险偏好会突然切换；
- 约束比模型假设更复杂；
- 过度优化会导致脆弱组合。

因此，金融中的优化必须和稳健性、约束、风险管理一起理解。

一个好的 AI 投研系统不只是“最大化预测准确率”，而是要优化整个投资决策流程。

## Research Corner

优化仍然是现代 AI 的开放问题。

值得长期思考：

1. 为什么 AdamW 在 Transformer 训练中如此常用？
2. SGD 与 Adam 的泛化差异来自哪里？
3. Learning rate schedule 为什么常常比优化器选择还重要？
4. 大模型 scaling 中，优化难度如何随模型规模变化？
5. 优化器是否只是训练工具，还是会影响模型最终学到的表示？
6. 金融 AI 中，如何设计稳健而非过拟合的优化目标？

未来学习 LLM training 时，你会反复遇到这些问题。

## Exercises

### Basic

1. 用自己的话解释 Optimizer 与 Gradient 的区别。
2. 为什么学习率太大会导致训练发散？
3. `loss.backward()` 和 `optimizer.step()` 分别做什么？

### Intermediate

1. 用 Python 实验不同学习率对 `L(w) = (w - 3)^2` 的影响。
2. 解释 SGD 为什么比 full-batch Gradient Descent 更有噪声。
3. Momentum 为什么可以减少震荡？

### Advanced

1. 解释 Adam 为什么需要保存额外状态。
2. 为什么优化器越强，不代表模型越符合真实目标？
3. 在金融组合优化中，为什么历史最优组合可能未来很差？

### Research

1. 如果训练 Loss 下降，但验证 Loss 上升，你会如何诊断？
2. 学习率 schedule 是否可以看作一种隐式正则化？
3. 优化器会不会影响模型内部表示的几何结构？

## Teach Back

请用 3 分钟向一个高中生解释：

> 为什么模型知道方向以后，还需要优化器？

要求：

- 用下山或骑车类比；
- 解释学习率；
- 说明为什么走太快和走太慢都不好。

## Chapter Summary

本章建立了优化的核心直觉：

- Loss 告诉模型当前有多差。
- Gradient 告诉模型往哪里改。
- Optimizer 决定如何使用梯度更新参数。
- Learning rate 是最重要的优化超参数之一。
- SGD 用小批量数据估计梯度，便宜但有噪声。
- Momentum 让优化器记住过去方向。
- Adam / AdamW 为不同参数自适应调整更新。
- 优化可能失败，尤其当学习率、Loss 或工程系统设计不当时。
- 金融优化与模型优化共享“目标、约束、更新”的思维。

## Master Insight

> 优化不是让模型知道答案，而是让模型在不完美的信息中，一步一步变得不那么错。

## Bridge to Next Chapter

现在我们已经有：

```text
Loss: 目标差距
Gradient: 局部方向
Optimizer: 更新策略
```

但还有一个更深的问题：

> 深层网络里，Loss 离前面的参数很远，梯度怎么传过去？

这需要链式法则。

下一章进入：

> Chapter 18: 为什么链式法则是深度学习的核心？
