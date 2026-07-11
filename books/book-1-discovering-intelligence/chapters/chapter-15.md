# Chapter 15: 为什么梯度能够告诉机器如何学习？

> Book I · Discovering Intelligence  
> Act II · 数学如何变成智能

## Learning Objectives

完成本章后，你应该能够回答：

- 为什么机器学习需要梯度。
- 梯度和导数的关系是什么。
- 为什么梯度表示局部最有效的改进方向。
- 为什么 `loss.backward()` 能产生参数的 `.grad`。
- 为什么梯度不是答案，而是改进建议。
- 为什么梯度会失效、爆炸或消失。

## Opening Story: 夜晚下山

想象你夜晚站在一座山上。

四周完全黑暗。

你看不见山谷在哪里，也看不见整座山的形状。

你只能做一件事：

> 用脚感受脚下地面的倾斜方向。

如果地面向左下方倾斜，你就往左走一点。

如果地面向右下方倾斜，你就往右走一点。

你不知道全局最优路线。但你知道当前这一小步，哪边更可能下降。

这就是梯度的直觉。

机器训练模型时也一样。它不知道最佳参数在哪里，只能根据当前位置的局部信息判断：

> 如果我稍微改变参数，Loss 会怎么变？

梯度就是这个局部改进信号。

## The One Sentence

> 梯度不是答案，而是模型在当前位置收到的“改进方向”。

## Why Before What

为什么需要梯度？

因为模型参数太多，不能靠随机试错。

一个现代模型可能有：

```text
1 million
100 million
10 billion
```

甚至更多参数。

如果每个参数都像一个旋钮，我们不可能随机拧每个旋钮，然后等着模型变好。

我们需要知道：

> 每个参数对 Loss 的影响方向和影响大小。

这就是梯度要回答的问题。

## Feynman Explanation

想象你在调一台有一百万个旋钮的机器。

机器会输出一个分数：

```text
Loss = 10.0
```

你希望 Loss 变小。

但你不知道该调哪个旋钮。

如果每个旋钮旁边都有一个小箭头：

```text
旋钮 1: 往左调
旋钮 2: 往右调
旋钮 3: 不用动
...
```

事情就变简单了。

梯度就是每个旋钮旁边的小箭头。

它告诉你：

> 这个参数往哪个方向动，会让 Loss 下降。

更准确地说，梯度告诉你 Loss 上升最快的方向。训练时我们反着走，所以叫梯度下降。

## Historical Background

梯度来自微积分，但它真正改变 AI，是因为它让大规模参数学习成为可能。

早期神经网络曾经长期难以训练。直到反向传播被系统化使用，人们才真正能够高效计算每个参数对最终误差的贡献。

1986 年，Rumelhart、Hinton 和 Williams 的反向传播工作让神经网络训练进入新阶段。

但反向传播背后的核心仍然是梯度：

```text
Loss 对每个参数的偏导数
```

今天 PyTorch、JAX、TensorFlow 的自动求导系统，本质上都是在自动完成这件事。

Karpathy 的 `micrograd` 之所以重要，是因为它把这个看似神秘的过程拆成了非常小的计算图和链式法则。

## First Principles

假设 Loss 只依赖一个参数：

```text
L = f(w)
```

导数回答：

```text
如果 w 稍微增加一点，L 会怎么变？
```

如果：

```text
dL/dw > 0
```

说明 `w` 增加会让 Loss 增加。

为了降低 Loss，我们应该减小 `w`。

如果：

```text
dL/dw < 0
```

说明 `w` 增加会让 Loss 减小。

为了降低 Loss，我们应该增大 `w`。

当参数很多时：

```text
theta = [w1, w2, w3, ...]
```

每个参数都有自己的偏导数：

```text
dL/dw1
dL/dw2
dL/dw3
...
```

把这些偏导数组合起来，就是梯度：

```text
grad L = [dL/dw1, dL/dw2, dL/dw3, ...]
```

所以梯度不是一个神秘概念。

它只是：

> 所有参数的局部影响力列表。

## Intuition: 梯度是责任分配

模型做错了，Loss 变大。

但谁负责？

是第一层的某个权重？

是最后一层的偏置？

是 embedding 的某个维度？

梯度在做一件非常重要的事：

> 把最终错误分配给每一个参数。

如果某个参数对错误影响很大，它的梯度就大。

如果某个参数几乎没有影响，它的梯度就小。

这就是为什么梯度能驱动学习。

它把一个整体错误拆成许多局部改进建议。

## Mathematics: 梯度下降的核心公式

训练时，参数更新通常写成：

```text
theta = theta - learning_rate * gradient
```

其中：

- `theta` 是参数；
- `gradient` 是 Loss 对参数的梯度；
- `learning_rate` 是每一步走多大。

为什么是减号？

因为梯度指向 Loss 增加最快的方向。

我们想让 Loss 下降，所以反着走。

如果只有一个参数：

```text
w_new = w_old - lr * dL/dw
```

这就是梯度下降最核心的思想。

## Visualization: Loss Surface

请想象一张地形图：

```text
Loss
  ▲
  │        *
  │       / \
  │      /   \
  │_____/     \____
  └────────────────► parameter
```

星号是当前参数位置。

斜率告诉你左边低还是右边低。

在高维空间中，我们不能画出完整地形，但逻辑相同。

梯度是当前位置的局部斜率。

## Coding Lab: 手写一个梯度下降

我们先不用 PyTorch。

目标函数：

```text
L(w) = (w - 3)^2
```

最小值显然在 `w = 3`。

```python
w = 0.0
lr = 0.1

for step in range(20):
    loss = (w - 3) ** 2
    grad = 2 * (w - 3)
    w = w - lr * grad
    print(step, w, loss)
```

观察 `w` 如何一步步靠近 3。

这就是学习的最小版本。

## PyTorch Preview

```python
import torch

w = torch.tensor(0.0, requires_grad=True)

loss = (w - 3) ** 2
loss.backward()

print(w.grad)
```

`w.grad` 中保存的就是：

```text
dL/dw
```

也就是 Loss 对参数 `w` 的梯度。

手动更新可以写成：

```python
with torch.no_grad():
    w -= 0.1 * w.grad
```

真实训练中，优化器会帮你做这个更新。

## Engineering Perspective

工程中，梯度有几个关键问题。

### Gradient accumulation

如果一个参数通过多条路径影响 Loss，它收到的梯度需要累加。

这就是为什么 `micrograd` 里常常使用：

```python
self.grad += ...
```

而不是：

```python
self.grad = ...
```

### Gradient zeroing

PyTorch 默认会累加梯度。

所以每一步训练前通常需要：

```python
optimizer.zero_grad()
```

否则上一轮梯度会混进来。

### Gradient clipping

如果梯度太大，训练可能发散。

这时可以使用梯度裁剪：

```python
torch.nn.utils.clip_grad_norm_(model.parameters(), max_norm=1.0)
```

### Mixed precision

大模型训练中，梯度常常与混合精度、loss scaling、分布式通信相关。

你现在不需要掌握所有工程细节，但要知道：

> 梯度是训练系统的血液。

## Failure Modes

### Failure 1: 梯度消失

在很深的网络里，梯度可能一层层变小，最后接近 0。

前面的层几乎学不到东西。

### Failure 2: 梯度爆炸

梯度可能变得非常大，导致参数更新过猛，Loss 发散。

### Failure 3: 局部最优

梯度下降可能进入局部低谷，难以找到更好的区域。

### Failure 4: 鞍点

在高维空间中，很多点不是最低点，而是某些方向上升、某些方向下降的鞍点。

梯度在这些区域可能很小，训练变慢。

### Failure 5: 错误 Loss 的正确梯度

如果 Loss 设计错了，梯度会非常认真地带模型走向错误目标。

所以梯度不是道德指南。它只服务于 Loss。

## AI x Finance

金融中的优化也依赖梯度思想。

假设你有一个投资组合，参数是每个资产的权重：

```text
theta = [w_stock1, w_stock2, w_stock3, ...]
```

目标可能是最大化风险调整后收益，或者最小化跟踪误差。

梯度可以告诉你：

> 哪个权重稍微增加，会让目标变好或变差？

当然，真实投资比标准梯度下降更复杂，因为市场会变化，交易成本存在，约束很多，目标也不稳定。

但核心直觉相同：

> 梯度是局部改进方向。

这对理解优化、组合构建和 AI 投研系统都非常重要。

## Research Corner

几个值得长期思考的问题：

1. 为什么大模型训练中梯度仍然如此有效？
2. 梯度下降是否只是优化工具，还是也与泛化能力有关？
3. 为什么 Adam、SGD、AdamW 会产生不同训练行为？
4. 梯度噪声是否帮助模型逃离坏的局部区域？
5. 在 RLHF 或偏好优化中，梯度到底来自什么信号？
6. 金融市场里的目标函数不稳定时，梯度优化是否可靠？

## Exercises

### Basic

1. 用自己的话解释梯度是什么。
2. 为什么训练时要沿着负梯度方向走？
3. 对 `L(w) = (w - 5)^2`，求 `dL/dw`。

### Intermediate

1. 写一个 Python 循环，用梯度下降最小化 `L(w) = (w + 2)^2`。
2. 解释为什么 PyTorch 训练中需要 `optimizer.zero_grad()`。
3. 为什么梯度太大或太小都会出问题？

### Advanced

1. 用自己的话解释梯度累加为什么需要 `+=`。
2. 解释梯度消失与 Sigmoid 饱和之间的关系。
3. 在金融优化里，为什么“局部最优”可能不是最大问题？

## Teach Back

请用 3 分钟向一个高中生解释：

> 梯度为什么像“下山方向”？

要求：

- 不从导数公式开始；
- 必须解释为什么要反着梯度走；
- 必须说明梯度和 Loss 的关系。

## Chapter Summary

本章建立了梯度的核心直觉：

- 梯度告诉参数如何局部改进。
- 梯度是 Loss 对参数的偏导数组成的向量。
- 梯度下降沿负梯度方向更新参数。
- `loss.backward()` 会计算计算图中各参数的梯度。
- 梯度可能消失、爆炸，也可能忠实优化错误目标。
- 梯度是连接 Loss、Optimization、Backpropagation 的关键桥梁。

## Master Insight

> 梯度把“模型错了”翻译成“每个参数应该如何改变”。

## Bridge to Next Chapter

梯度回答：

```text
往哪里改？
```

但它没有回答：

```text
为什么要改？
```

这个“为什么”来自 Loss。

下一章我们将学习：

> Chapter 16: 为什么需要损失函数（Loss Function）？
