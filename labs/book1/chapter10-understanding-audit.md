# Chapter 10 Understanding Audit

先写含义，再写符号。只给公式、不给现实对象与边界的答案不算通过。

## Explain

1. 为什么数学是一种关系语言，而不只是计算？
2. Precision 与 Accuracy 有什么不同？
3. 为什么公式可以完全算对，却回答了错误问题？

## Predict

模型：$y=2x+10$，其中 $x$ 是“广告投入”，但团队没有写单位和时间窗口。

1. 分别假设 $x$ 以元、万元和点击数计量，预测 $w=2$ 的含义怎样变化；
2. 检查 $x=0$ 与极大 $x$ 的 Limiting Case；
3. 写出一个让线性关系失效的 Boundary；
4. 指出哪些错误不会被 Arithmetic Test 发现。

## Reconstruct

将“相似用户应该得到相似推荐”翻译为：

```text
Object → Relation → Operation → Assumption → Quantity → Test → Boundary
```

然后从你的公式反向恢复自然语言，不允许引入翻译时未声明的新含义。

## Transfer

选择医疗风险、物理运动或 Finance Score：

1. 定义 Object、Unit 与 Time Boundary；
2. 写出最小关系；
3. 执行 Units、Limit 与 Perturbation 检查；
4. 指出 Proxy Substitution；
5. 写出会反驳模型关系的 Observation。

## Passing Standard

- Meaning Before Symbols；
- 能区分 Definition、Assumption、Derivation 与 Observation；
- 能从错误结论追踪到 Translation Failure；
- 能解释一个公式何时失效；
- 能说明为什么下一章需要多维 Vector。

