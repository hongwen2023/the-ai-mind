# Chapter 3 Learning Package

## Chapter

[为什么抽象是人类最重要的工具之一？](../chapters/chapter-03.md)

## One Sentence

> **抽象不是把细节删掉，而是为一个目的保留足够重要的关系。**

## Book I Question

```text
Relationship
  → Generation
  → Abstraction
  → Representation
  → Learning
```

Chapter 3 studies how a task-specific contract makes generated complexity
manageable. Chapter 4 asks how the retained relationships become a form a
machine can store and transform.

## Notebook

[Abstraction Boundary Lab](../../../notebooks/book1/chapter03_abstraction_boundary.ipynb)

Use it to replace implementations, violate units, collapse error states, and
observe abstraction leakage. Write a prediction before each run.

## Understanding Audit

[Chapter 3 Understanding Audit](../../../labs/book1/chapter03-understanding-audit.md)

The Audit verifies Explain, Predict, Reconstruct, and Transfer separately.

## Figures

- [One Reality, Different Abstractions](../../../figures/book1/chapter03/one-reality-many-abstractions.svg)
- [Abstraction Contract](../../../figures/book1/chapter03/abstraction-contract.svg)

## Suggested Order

1. Read through Purpose / Interface / Invariant / Hidden Detail.
2. Reconstruct the object-grouping diagram before reading the formulas.
3. Predict every Contract perturbation before running the Notebook.
4. Build two finance abstractions for different decision horizons.
5. Complete Common Illusions and Research Corner.
6. Complete the Understanding Audit without the chapter open.
7. Repeat reconstruction after seven days.

## Mental Model Upgrade

```text
Before: abstraction = fewer details.

After:  abstraction = task-specific contract
        + preserved relationships
        + hidden implementation
        + known boundary.
```

The upgrade is complete only when the learner can change the abstraction when
the task changes, choose an appropriate abstraction level, and predict which
hidden distinction will matter. The goal is reliable reasoning at lower cost,
not the highest possible abstraction layer.

## Capability Milestone

After this package, the learner can:

- [ ] **Explain** abstraction as a task-specific contract.
- [ ] **Predict** which contract change breaks a dependent system.
- [ ] **Build** and perturb an interface with replaceable implementations.
- [ ] **Read** a model claim for hidden assumptions and lost distinctions.
