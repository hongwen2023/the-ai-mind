# Chapter 4 Understanding Audit

Complete this audit without the chapter open. Record uncertainty explicitly.

## Explain

1. 分离 Reality、Observation、Representation 与 Model。
2. 为什么“已经数字化”不等于“已经形成好表示”？
3. 用自己的话解释：Geometry 是表示赋予的邻近、距离与方向。

## Predict

1. weekday 使用 `0` 到 `6` 的 ordinal encoding，线性模型会怎样看待 Sunday 与 Monday？
2. missing 与 genuine zero 都编码为 `0`，哪两类下游错误最可能发生？
3. 公司特征从 raw scale 改成 standardized ratios，最近邻为什么会变化？

## Reconstruct

从空白页重建：

```text
Reality → Observation → Encoding → Representation → Model
```

以及：

\[
R:O\rightarrow Z
\]

\[
\hat{y}=f(R(o))
\]

\[
o_1\neq o_2,
\qquad
R(o_1)=R(o_2)
\]

最后重建 Observation / Encoding / Distinction / Geometry / Operation 五项审计。

## Transfer

选择医疗、供应链、教育或法律中的一个对象：

- 为两个不同任务设计不可互换的表示；
- 指出一个 representation collision；
- 解释距离或邻近的含义；
- 写出一个会造成 leakage 的时间边界错误。

## Evidence Standard

The audit is complete only if the learner can:

- change the representation when the task changes;
- predict a geometry change before running code;
- distinguish missingness from a genuine value;
- identify information that no downstream model can recover.
