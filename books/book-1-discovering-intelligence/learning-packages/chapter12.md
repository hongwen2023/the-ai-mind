# Chapter 12 Learning Package

## Chapter

[为什么矩阵能够描述变化？](../chapters/chapter-12.md)

## One Sentence

> **Matrix 是 Input-output Transformation Contract。**

## Notebook

[Mix, Trace, Compose](../../../notebooks/book1/chapter12_matrices.ipynb)

先用 Equation 预测每个 Output，再用 `A @ x` 验证。所有 Perturbation 必须同时记录 Row Recipe、Column Influence、Shape 与 Unit。

## Understanding Audit

[Chapter 12 Understanding Audit](../../../labs/book1/chapter12-understanding-audit.md)

## Figure

[Matrix Transformation Audit](../../../figures/book1/chapter12/matrix-transformation-audit.svg)

## Mental Model Upgrade

```text
Before: matrix = rectangular table + row times column.

After:  matrix = input-output contract + row recipes
        + column influence + shape semantics + ordered composition.
```

Transformation Contract 描述关系，不自动证明 Causal Mechanism。二维网格也只是帮助建立 Geometry 直觉，不覆盖全部高维 Matrix。

## Capability Milestone

- [ ] **Explain** Shape、Rows、Columns 与 Composition；
- [ ] **Predict** Input Influence 与 Transformation Failure；
- [ ] **Build** Matrix Transformation Contract；
- [ ] **Read** Shape Match 下的语义错误。
