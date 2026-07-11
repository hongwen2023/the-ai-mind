# Chapter 3 Understanding Audit

Complete this audit without the chapter open. Record uncertainty instead of
guessing silently.

## Explain

1. 不使用“简化”和“概括”，解释为什么抽象是一份带目的的契约。
2. 解释 Purpose、Interface、Invariant 与 Hidden Detail 各自解决什么问题。
3. 为什么“好的抽象降低推理成本”不等于“现实变简单”？

## Predict

一个函数把错误、缺失值和真实零值都返回为 `0`：

1. 预测两个不同调用者可能出现的错误；
2. 指出被错误合并的具体状态；
3. 写出一个更诚实的接口 Contract。

## Reconstruct

从空白页重建：

```text
concrete states X
  → abstraction A
  → abstract states Z
  → task decision h
```

然后写出并解释：

\[
A:X\rightarrow Z
\]

\[
x_1\sim_A x_2
\quad\text{when}\quad
A(x_1)=A(x_2)
\]

\[
g(x)\approx h(A(x))
\]

## Transfer

选择医疗、制造、教育、法律或供应链中的一个问题：

- 定义任务；
- 设计接口；
- 写出一个 Invariant；
- 指出隐藏了什么；
- 设计一个会迫使使用者下钻的边界案例。

## Evidence Standard

The audit is complete only if the learner can:

- change the abstraction when the task changes;
- predict a failure before running a perturbation;
- distinguish implementation replacement from contract violation;
- name evidence that would reveal a lost distinction.
