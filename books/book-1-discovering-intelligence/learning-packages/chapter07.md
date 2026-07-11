# Chapter 7 Learning Package

## Chapter

[为什么好的模型能够举一反三？](../chapters/chapter-07.md)

## One Sentence

> **泛化是在明确的新情境边界内，让学到的关系继续产生可靠结果。**

## Notebook

[Fit, Hold Out, Shift](../../../notebooks/book1/chapter07_generalization.ipynb)

Predict Degree, coverage, holdout, and extrapolation behavior before running.

## Understanding Audit

[Chapter 7 Understanding Audit](../../../labs/book1/chapter07-understanding-audit.md)

## Figures

- [Generalization Audit](../../../figures/book1/chapter07/generalization-audit.svg)
- [Fit, Holdout, Shift](../../../figures/book1/chapter07/fit-holdout-shift.svg)

## Mental Model Upgrade

```text
Before: generalization = high test score.

After:  generalization claim = independent boundary + specified shift
        + relevant metric + uncertainty + failure analysis.
```

More test sets do not automatically strengthen evidence. Independence is lost
when repeated evaluation guides model, prompt, feature, or threshold choices.

## Capability Milestone

- [ ] **Explain** Memorization, Shortcut, and bounded Generalization.
- [ ] **Predict** how Split and Shift alter evidence.
- [ ] **Build** a Train/Holdout/Shift experiment.
- [ ] **Read** claims for Leakage, Coverage, and Metric blind spots.
