# Chapter 6 Understanding Audit

Complete this audit without the chapter open.

## Explain

1. 不使用 Gradient、Backpropagation 或 Optimizer，解释机器为什么能够学习。
2. 为什么参数变化、保存日志和训练分数提高都不足以单独证明学习？
3. 为什么 Feedback 与 Credit Assignment 必须分开？

## Predict

预测 rate 为零、rate 过大、错误标签、无 Retention、单点数据和反馈错配各自怎样改变未来行为。

## Reconstruct

重建七阶段 Learning Audit，以及：

\[
\hat y_t=f_{\theta_t}(x_t),\quad
e_t=E(\hat y_t,y_t),\quad
\theta_{t+1}=U(\theta_t,x_t,e_t)
\]

说明 Parameter Change、Learning Evidence 与 Generalization 的区别。

## Transfer

选择一个组织流程或 Agent Workflow：指出 Feedback、Credit、Update 与 Retention，并设计测试判断未来行为是否真正改变。

## Evidence Standard

The audit is complete only if the learner can trace feedback into future
behavior, identify a credit path, and reserve unseen experience for Chapter 7's
generalization test.
