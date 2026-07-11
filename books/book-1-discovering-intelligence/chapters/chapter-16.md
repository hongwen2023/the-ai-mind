# Chapter 16: 为什么需要损失函数（Loss Function）？

> Book I · Discovering Intelligence  
> Act II · 数学如何变成智能

## Learning Objectives

完成本章后，你应该能够回答：

- 为什么机器学习必须有一个“好坏标准”。
- Loss Function 与 Accuracy 的区别是什么。
- 为什么模型优化的通常不是“正确率”，而是 Loss。
- 为什么不同任务需要不同的 Loss。
- 为什么 Loss 是 Gradient Descent、Backpropagation 和 Autograd 的起点。
- 为什么一个设计不好的 Loss 会让模型学会错误的目标。

## Opening Story: 没有分数，就没有学习

想象你第一次练习射箭。

你站在靶子前，拉弓，射出第一箭。

你问教练：

> 我射得怎么样？

教练说：

> 继续。

你射出第二箭。

你又问：

> 这次呢？

教练还是说：

> 继续。

你射出第三箭、第四箭、第五箭。教练始终只说同一句话：

> 继续。

请问，你会进步吗？

很难。

不是因为你不努力，而是因为你没有反馈。你不知道哪一箭离靶心更近，也不知道自己是在变好还是变差。你甚至不知道“好”到底是什么意思。

学习需要反馈。更准确地说，学习需要一个可以衡量进步的信号。

在机器学习里，这个信号叫：

> Loss Function，损失函数。

它不是模型的答案。它是模型离答案还有多远的度量。

## The One Sentence

> Loss Function 的作用不是告诉模型正确答案，而是告诉模型：它现在离目标还有多远。

## Why Before What

在开始定义 Loss Function 之前，先问一个更根本的问题：

> 如果机器做错了，它怎么知道自己错了多少？

只知道“错了”是不够的。

假设有一个猫狗分类器。真实标签是“猫”。

模型 A 输出：

```text
猫: 0.51
狗: 0.49
```

模型 B 输出：

```text
猫: 0.99
狗: 0.01
```

如果只看 Accuracy，它们都是“正确”。

但显然，模型 B 更好。它不只是猜对了，而且很有把握。

再看两个错误例子。真实标签仍然是“猫”。

模型 C 输出：

```text
猫: 0.49
狗: 0.51
```

模型 D 输出：

```text
猫: 0.001
狗: 0.999
```

如果只看 Accuracy，它们都是“错误”。

但模型 C 只是差一点，模型 D 则极其自信地错了。

机器学习不能只需要“对”或“错”。它需要一个连续的评分系统，能够区分：

- 差一点对；
- 非常确定地对；
- 差一点错；
- 非常确定地错。

这就是 Loss Function 出现的根本原因。

## Feynman Explanation

把模型想象成一个蒙着眼睛投飞镖的人。

它不知道靶心在哪里，只能每次投完之后得到一个数字：

```text
距离靶心 32 厘米
距离靶心 18 厘米
距离靶心 9 厘米
距离靶心 4 厘米
```

这个数字不是答案。它只是距离。

但这个距离足够重要。因为只要距离越来越小，模型就知道自己在进步。

Loss 就是这个距离。

训练模型时，我们真正做的事情不是直接告诉模型：

> 你应该成为一个聪明模型。

而是不断告诉它：

> 这一次离目标还有多远。

然后模型通过梯度，判断参数应该往哪里改，才能让这个距离变小。

这就是现代机器学习最核心的闭环：

```text
Prediction
  ↓
Loss
  ↓
Gradient
  ↓
Update
  ↓
Better Prediction
```

## Historical Background

早期的人工智能有一种强烈倾向：人类试图直接写规则。

例如：

```text
如果图像里有尖耳朵和胡须，那么可能是猫。
```

这种方式的问题很明显。现实世界太复杂，规则永远写不完。

机器学习改变了这个思路。它不再要求人类写出所有规则，而是让模型从数据中调整自己。

但一旦允许模型自己调整，就必须回答一个问题：

> 调整以后，怎么知道变好了？

这就是 Loss 的历史地位。

Loss Function 把“模型表现”变成一个数字。只要表现能变成数字，就可以优化。只要可以优化，就可以使用梯度下降。只要可以使用梯度下降，就可以训练大规模神经网络。

所以 Loss 不是一个小工具。它是把学习变成数学问题的入口。

## First Principles

机器学习训练中有四个基本对象：

```text
Parameters
Prediction
Loss
Update
```

参数决定模型如何预测。

预测产生输出。

Loss 衡量输出与目标之间的差距。

Update 根据 Loss 的梯度修改参数。

更抽象地说：

```text
Model:       y_hat = f(x; theta)
Loss:        L(y_hat, y)
Training:    find theta that makes L small
```

其中：

- `x` 是输入；
- `y` 是真实目标；
- `y_hat` 是模型预测；
- `theta` 是模型参数；
- `L` 是 Loss Function。

训练的核心目标可以写成：

```text
minimize L(y_hat, y)
```

也就是：

> 找到一组参数，让模型的预测与真实目标之间的差距尽可能小。

这句话非常重要。

机器不是直接学习“世界”。机器学习的是：

> 如何让某个 Loss 下降。

如果 Loss 设计得好，模型学到的东西会接近我们想要的能力。

如果 Loss 设计得不好，模型会忠实地优化错误目标。

## Loss vs Accuracy

很多初学者会问：

> 既然最终关心准确率，为什么训练时不用 Accuracy？

原因是 Accuracy 太粗糙。

Accuracy 通常是离散的：

```text
correct: 1
wrong:   0
```

它告诉我们最终有没有答对，但很难告诉参数应该怎么改。

Loss 通常是连续的。

连续信号的好处是可以产生梯度。

梯度需要回答：

> 如果某个参数稍微变一点，Loss 会怎么变？

Accuracy 很难回答这个问题。

Loss 可以。

这就是为什么训练时常常优化 Loss，而评估时才看 Accuracy、F1、AUC、BLEU、ROUGE、win rate 等指标。

## Mathematics: 最简单的 Loss

先看一个回归问题。

真实值是：

```text
y = 10
```

模型预测：

```text
y_hat = 7
```

误差是：

```text
error = y_hat - y = -3
```

最直接的 Loss 可以是平方误差：

```text
L = (y_hat - y)^2
```

代入：

```text
L = (7 - 10)^2 = 9
```

为什么要平方？

第一，平方可以让正误差和负误差都变成正数。

第二，平方会惩罚更大的错误。

例如：

```text
error = 1  -> loss = 1
error = 2  -> loss = 4
error = 10 -> loss = 100
```

这意味着模型如果犯了大错，会受到更强惩罚。

这就是 Mean Squared Error（MSE）的直觉。

## Classification Loss: 为什么分类更麻烦？

分类问题不只是预测一个数字，而是预测一个概率分布。

例如真实标签是“猫”，模型输出：

```text
猫: 0.8
狗: 0.2
```

另一个模型输出：

```text
猫: 0.51
狗: 0.49
```

它们都预测“猫”，但第一个更好。

分类 Loss 需要奖励模型把概率放在正确类别上。

最常见的选择是 Cross Entropy。

对单个正确类别来说，核心形式是：

```text
loss = -log(p_correct)
```

如果模型给正确类别的概率很高：

```text
p_correct = 0.9
loss = -log(0.9) ≈ 0.105
```

如果模型给正确类别的概率很低：

```text
p_correct = 0.01
loss = -log(0.01) ≈ 4.605
```

这非常符合直觉：

- 越相信正确答案，Loss 越小；
- 越不相信正确答案，Loss 越大；
- 如果极其自信地错了，Loss 会很大。

这也是 Karpathy 在 `makemore` 里反复强调负对数似然的原因。

语言模型训练中，本质上也是在问：

> 给定前面的 token，模型给下一个正确 token 分配了多少概率？

如果概率高，Loss 小。

如果概率低，Loss 大。

## Visualization: Loss Landscape

请想象一张地形图。

横轴和纵轴表示模型的两个参数。

高度表示 Loss。

```text
high loss
    ▲
    │       /\ 
    │      /  \      __
    │  ___/    \____/  \__
    │_/                    \___
    └──────────────────────────► parameters
                         low loss
```

训练模型就像在这张地形图上找低谷。

Loss 告诉我们当前所在位置有多高。

Gradient 告诉我们哪边下坡最快。

Optimizer 决定每一步怎么走。

这三个概念不能分开理解：

```text
Loss:      当前有多差
Gradient:  往哪边改
Optimizer: 怎么迈步
```

下一章的 Optimization 就是在回答第三个问题。

## Coding Lab: 用 Python 感受 Loss

下面用最简单的 Python 实验观察平方误差。

```python
def mse_loss(y_hat, y):
    return (y_hat - y) ** 2

y = 10

for y_hat in [0, 5, 8, 9, 10, 11, 12, 15, 20]:
    print(y_hat, mse_loss(y_hat, y))
```

你会看到，预测越接近 10，Loss 越小。

接下来观察 Cross Entropy 的直觉：

```python
import math

def ce_loss(p_correct):
    return -math.log(p_correct)

for p in [0.99, 0.9, 0.7, 0.5, 0.1, 0.01]:
    print(p, ce_loss(p))
```

你应该注意到：

- 当正确概率接近 1，Loss 接近 0；
- 当正确概率很小，Loss 会快速变大。

这就是分类模型训练的核心信号。

## PyTorch Preview

在 PyTorch 里，Loss 通常是一个函数或模块：

```python
import torch
import torch.nn as nn

pred = torch.tensor([2.5], requires_grad=True)
target = torch.tensor([3.0])

loss_fn = nn.MSELoss()
loss = loss_fn(pred, target)

loss.backward()

print(loss.item())
print(pred.grad)
```

这段代码展示了整个训练世界的核心：

```text
prediction
  ↓
loss
  ↓
backward
  ↓
gradient
```

注意：`loss.backward()` 不是魔法。

它只是从 Loss 出发，沿着计算图反向传播，把每个参数对 Loss 的影响算出来。

这会在 Chapter 18 和 Chapter 19 里展开。

## Engineering Perspective

在真实 AI 工程中，Loss 不是随便选的。

不同任务需要不同 Loss：

| Task | Common Loss | Why |
|---|---|---|
| 回归 | MSE / MAE | 衡量数值预测误差 |
| 二分类 | Binary Cross Entropy | 衡量正确类别概率 |
| 多分类 | Cross Entropy | 训练概率分布 |
| 语言模型 | Next-token Cross Entropy | 预测下一个 token |
| 检索 | Contrastive Loss | 拉近相似样本，推远不相似样本 |
| 强化学习 | Policy / Value Loss | 优化行动策略 |
| RLHF / DPO | Preference-based objective | 对齐人类偏好 |

工程师真正要问的是：

> 我选择的 Loss，是否真的代表我想让模型学会的东西？

很多失败的 AI 系统不是模型不够大，而是目标函数不对。

## Failure Modes: Loss 会骗你

Loss 很重要，但 Loss 也危险。

因为模型会非常忠实地优化你给它的目标，即使那个目标不是你真正想要的。

### Failure 1: Proxy mismatch

你真正关心用户满意度，但训练 Loss 只是点击率。

模型可能学会制造标题党。

点击率上升，用户体验下降。

### Failure 2: Low loss, bad behavior

语言模型的 next-token loss 很低，说明它很会预测文本。

但这不等于它诚实、安全、有帮助。

所以后面还需要 instruction tuning、RLHF、DPO、evaluation。

### Failure 3: Class imbalance

如果 99% 样本都是正常交易，1% 是欺诈交易。

模型永远预测“正常”，Accuracy 可以达到 99%。

但它完全没有学会识别欺诈。

这时普通 Accuracy 和普通 Loss 都可能误导你。

### Failure 4: Outliers

MSE 会强烈惩罚大误差。

这在很多场景很好，但如果数据里有极端异常值，模型可能被少数离群点拖着走。

这时 MAE、Huber Loss 或更稳健的目标函数可能更合适。

## AI x Finance

金融研究里，Loss 的思想无处不在。

假设你在做一个盈利预测模型。

你可以用：

```text
prediction = next quarter EPS
target = actual EPS
loss = prediction error
```

但这还不够。

因为投资真正关心的可能不是 EPS 预测误差，而是：

- 股价反应；
- 超额收益；
- 风险调整后收益；
- 回撤；
- 胜率；
- 信息比率；
- 组合稳定性。

如果你只优化 EPS 误差，模型可能成为一个很好的财务预测器，但不是一个好的投资模型。

这就是 Loss 设计在 AI 投研里的核心问题：

> 你到底想优化什么？

在 AI Hedge Fund Research Platform 里，Loss 不只是技术选择。它是投资哲学的数学表达。

## Research Corner

Loss Function 今天仍然是 AI 研究的中心问题之一。

几个值得长期思考的问题：

1. Next-token prediction 是否足以产生通用智能？
2. 为什么语言模型的训练 Loss 下降，不一定意味着推理能力可靠提升？
3. 如何设计更接近人类偏好的 Loss？
4. Reward Model 本身是否只是另一种不完美的 Loss？
5. DPO、RLHF、GRPO 等方法，本质上如何重新定义“模型应该优化什么”？
6. 在金融 AI 中，如何避免模型优化短期指标，却损害长期收益？

未来学习 LLM alignment 时，你会发现很多看似高级的问题，本质上都回到同一个根：

> 我们究竟应该让模型最小化什么？

## Exercises

### Basic

1. 用自己的话解释：为什么 Accuracy 不适合作为训练神经网络的主要目标？
2. 计算 MSE：真实值为 5，预测值分别为 2、4、5、8 时，Loss 是多少？
3. 如果正确类别概率分别为 0.9、0.5、0.1，Cross Entropy 的大小顺序是什么？

### Intermediate

1. 举一个例子说明：Loss 下降但真实业务目标变差。
2. 为什么 MSE 对异常值敏感？
3. 为什么语言模型通常使用 next-token cross entropy？

### Advanced

1. 设计一个金融预测任务，并说明你会选择什么 Loss。
2. 如果你要训练一个投资 memo 生成模型，普通 next-token loss 有什么不足？
3. 为什么“优化用户点击”可能不是一个好的推荐系统目标？

### Research

1. 如果没有人工标签，模型能否构造自己的 Loss？
2. Preference optimization 是否可以看作一种新的 Loss 设计？
3. 如果一个模型在训练 Loss 上持续变好，但实际推理能力不稳定，你会如何诊断？

## Teach Back

请尝试用 3 分钟向一个高中生解释：

> Loss Function 为什么是机器学习里的“成绩单”？

要求：

- 不使用公式；
- 必须举一个生活例子；
- 必须说明 Loss 和 Gradient 的关系。

如果你能讲清楚这一点，你已经真正理解了本章的核心。

## Chapter Summary

本章建立了 Loss Function 的核心直觉：

- 机器学习需要反馈。
- Loss 把“表现好坏”变成连续数字。
- Accuracy 适合评估，但通常不适合训练。
- 回归常用 MSE，分类常用 Cross Entropy。
- Loss 是 Gradient Descent 的起点。
- Loss 设计错误，模型会优化错误目标。
- 在 AI 工程和金融 AI 中，选择 Loss 等于选择学习方向。

## Master Insight

> Loss 是机器学习的目标语言。模型不会自动学习“我们真正想要的东西”，它只会努力降低我们写下来的 Loss。

## Bridge to Next Chapter

现在我们已经有了两个关键概念：

```text
Loss: 当前离目标有多远
Gradient: 往哪里改能让 Loss 下降
```

但还缺一个问题：

> 每次应该改多少？

走得太小，学习很慢。

走得太大，可能越过低谷，甚至发散。

这就是下一章的主题：

> Chapter 17: 为什么优化能够让模型越来越好？
