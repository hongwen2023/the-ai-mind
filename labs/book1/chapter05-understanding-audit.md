# Chapter 5 Understanding Audit

Complete this audit without the chapter open.

## Explain

1. 不使用 CPU 或算术，解释计算为什么是可追踪的状态变换。
2. 为什么 State 是影响未来计算的信息，而不等于存储硬件？
3. 为什么复杂计算不自动等于智能？

## Predict

1. 交换 `deposit` 与 `withdraw` 的顺序，首个 Trace 分歧在哪里？
2. 相同算法依赖未记录缓存时，为什么系统结果可能不可复现？
3. 限制 `max_steps` 后，输出代表完整算法还是资源截断执行？

## Reconstruct

从空白页重建：

- Input / State / Rule / Order / Resource / Trace；
- (s_{t+1}=F(s_t,x_t))；
- (y=G(s_T))；
- Composition / Branch / Iteration / Memory；
- computable / feasible / learned / reliable 四层区别。

## Transfer

选择一个供应链、医疗或数据 Pipeline：

- 写出一条具体执行 Trace；
- 指出一个隐藏 State；
- 指出一个顺序依赖；
- 给出资源预算；
- 设计一个“输出相同但过程不可信”的反例。

## Evidence Standard

The audit is complete only if the learner can locate the first divergent
state, separate algorithm from execution, and explain why a wrong objective
can be computed perfectly.
