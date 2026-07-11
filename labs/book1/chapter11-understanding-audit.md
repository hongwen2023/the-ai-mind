# Chapter 11 Understanding Audit

所有 Geometry 结论必须声明 Coordinate Contract。只计算数字、不解释语义不算通过。

## Explain

1. 为什么 `[3, 5, 7]` 不自动成为 Semantic Vector？
2. 为什么 Distance 不是天然 Similarity？
3. Scalar Score 与 Vector 分别保留、丢失什么？

## Predict

Company A、B、C 使用 `[revenue, growth, margin]`：

1. Revenue 以美元、其他维度以百分比时，哪一维支配 Distance？
2. Standardize 后最近邻可能怎样变化？
3. 重复 Margin Dimension 会发生什么？
4. 交换 Growth 与 Margin 顺序但不改 Schema，会产生什么 Silent Failure？

## Reconstruct

从空白页重建：

- Vector Representation Audit；
- $mathbf{x}\in\mathbb{R}^d$；
- Difference、Magnitude、Distance、Dot Product 与 Cosine；
- 每个公式的现实含义与边界。

## Transfer

为文本、医疗或 Finance 设计 Vector：

1. 定义 Object、Coordinate、Order、Unit 与 Missing Policy；
2. 选择 Metric 并说明任务；
3. 写出一个 Collision 与一个 Semantic Overclaim；
4. 说明哪些现实信息未进入 Vector；
5. 设计一个 Perturbation Test。

## Passing Standard

- 能从任务建立 Coordinate Contract；
- 能手算并解释核心 Operation；
- 能在运行前预测 Scale 和 Metric 后果；
- 能区分模型 Geometry 与现实关系；
- 能说明为什么 Matrix 是下一步。

