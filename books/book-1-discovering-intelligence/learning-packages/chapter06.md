# Chapter 6 Learning Package

## Chapter

[为什么机器能够学习？](../chapters/chapter-06.md)

## One Sentence

> **学习让经验中的反馈改变未来计算，并产生可验证的行为改善。**

## Notebook

[Feedback-to-Update Lab](../../../notebooks/book1/chapter06_feedback_to_update.ipynb)

Perturb update rate, labels, retention, coverage, and feedback alignment.
Predict parameter direction and future behavior before every run.

## Understanding Audit

[Chapter 6 Understanding Audit](../../../labs/book1/chapter06-understanding-audit.md)

## Figures

- [Learning Loop](../../../figures/book1/chapter06/learning-loop.svg)
- [Credit Assignment](../../../figures/book1/chapter06/credit-assignment.svg)

## Mental Model Upgrade

```text
Before: learning = more data, stored examples, or changed parameters.

After:  learning = feedback-driven retained change
        + credit assignment + update mechanism
        + evidence of improved future behavior.
```

## Capability Milestone

- [ ] **Explain** Learning versus Execution, Memory, and random change.
- [ ] **Predict** how feedback quality and updates alter future behavior.
- [ ] **Build** a minimal feedback-driven learner without Autograd.
- [ ] **Read** a learning loop for Credit, Retention, and objective mismatch.
