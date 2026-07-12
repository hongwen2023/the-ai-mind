# Chapter 12 Understanding Audit

答案必须包含 Input/Output Object、Shape 与 Unit。只给数值结果不算通过。

## Explain

1. 为什么 Matrix 不只是数字表格？
2. Row View 与 Column View 分别回答什么？
3. Shape Match 为什么不保证 Semantic Match？

## Predict

给定三支麦克风到两个扬声器的 Matrix：

1. 只提高第二个 Input，哪些 Output 变化？
2. 交换 Input 1 和 2，但不交换 Column，会发生什么？
3. Transpose 后 Shape 与 Object Contract 怎样变化？
4. 先 Scaling 再 Mixing，与反向顺序是否相同？

## Reconstruct

1. 从三条 Output Equation 构造 Matrix；
2. 写出 $A\in\mathbb{R}^{m\times n}$ 的空间含义；
3. 从每个 Row 恢复 Output Equation；
4. 从每个 Column 解释 Input Influence；
5. 为每个 Entry 补 Unit。

## Transfer

选择 Feature Layer、医疗风险或 Factor Exposure：

1. 声明 Input/Output Coordinate；
2. 建立 Matrix 与 Shape Contract；
3. 写一个 Shape-compatible Semantic Failure；
4. 设计 Composition-order Test；
5. 声明 Linear 与 Information Boundary。

## Passing Standard

- 能在两种视角下解释 $A\mathbf{x}$；
- 能从关系构造 Matrix，而非只手算；
- 能预测 Row/Column 与 Order Perturbation；
- 能区分 Shape 与语义；
- 能说明为什么下一章需要 Linear Transformation 概念。

