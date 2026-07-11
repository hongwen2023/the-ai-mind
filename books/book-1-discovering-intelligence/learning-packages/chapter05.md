# Chapter 5 Learning Package

## Chapter

[为什么计算能够产生智能？](../chapters/chapter-05.md)

## One Sentence

> **计算把静态表示变成可追踪的新状态；智能还需要目标、反馈与学习。**

## Book I Question

```text
Relationship → Generation → Abstraction → Representation → Computation → Learning
```

Chapter 5 makes represented relationships executable. Chapter 6 asks how
feedback changes future computation.

## Notebook

[State Transition and Trace Lab](../../../notebooks/book1/chapter05_state_transition_trace.ipynb)

Perturb event order, initial state, precision, trace, and resource limits.
Predict the final output and first divergence before every run.

## Understanding Audit

[Chapter 5 Understanding Audit](../../../labs/book1/chapter05-understanding-audit.md)

## Figures

- [State Transition Trace](../../../figures/book1/chapter05/state-transition-trace.svg)
- [Computation Structures](../../../figures/book1/chapter05/computation-structures.svg)

## Suggested Order

1. Reconstruct the brick-factory six-question framework.
2. Hand-calculate the state table before reading the formulas.
3. Predict every Notebook perturbation before execution.
4. Audit one point-in-time finance Pipeline.
5. Complete Common Illusions and Research Corner.
6. Complete the Understanding Audit without the chapter open.

## Mental Model Upgrade

```text
Before: computation = arithmetic on faster hardware.

After:  computation = representation transformation
        + state + control flow + composition
        + resource limits + observable trace.
```

## Capability Milestone

- [ ] **Explain** computation as stateful representation transformation.
- [ ] **Predict** the first divergence caused by order, state, or resource changes.
- [ ] **Build** a small traceable state machine.
- [ ] **Read** an AI or finance computation for hidden state, lineage, and feasibility.
