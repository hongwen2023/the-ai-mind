# Chapter 8 Understanding Audit

先独立完成，再回看正文。每个答案必须包含证据边界，不能只写结论。

## Explain

1. 为什么一个合理解释仍不等于研究结论？
2. Observation 与 Interpretation 的边界在哪里？
3. 为什么 Ablation 降分不自动证明模块负责某项能力？

## Predict

一个文本分类器在训练和测试中都表现很好，但所有正面评论都包含感叹号。

1. 写出 H1“模型理解语义”和 H2“模型利用标点”的预测；
2. 设计一个只改变关键关系的 Intervention；
3. 在运行前写出三种可能结果及 Evidence Update。

## Reconstruct

不看正文，重建：

```text
Observation → Alternatives → Prediction → Intervention → Measurement → Update
```

并解释 Reproducibility 为什么横跨整个流程。

## Transfer

选择一个 Earnings Miss、医疗模型失败或 Agent 成功案例：

1. 分离 Observation 与解释；
2. 提出至少三个竞争假设；
3. 为每个假设写 Forward Prediction；
4. 设计一个能区分至少两个假设的测量或干预；
5. 写出什么结果会使你改变当前判断。

## Passing Standard

- 能提出真正竞争而非同义改写的解释；
- 能设计让解释预测分叉的条件；
- 能声明 Metric、Control 与不确定性；
- 能写出削弱自己首选解释的结果；
- 能把 Negative Result 转化为更精确的问题。

