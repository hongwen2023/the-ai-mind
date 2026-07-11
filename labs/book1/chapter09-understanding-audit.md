# Chapter 9 Understanding Audit

本 Audit 必须先闭卷完成。标准图只用于第二轮 Repair，不用于第一轮临摹。

## Pass 1 · Closed-book Reconstruction

1. 写出 Chapters 1–8 的核心节点，不看目录；
2. 连接你认为必要的 Edge；
3. 为每条 Edge 写一个关系动词；
4. 标记 Direction、Boundary、Evidence 和 Unknown；
5. 用五分钟口头解释整张图。

## Pass 2 · Stress Test

依次注入：

- Representation Collision；
- Wrong Edge；
- Feedback Delay；
- Test Leakage；
- Confounded Ablation。

对每项写出首个损坏位置、下游症状、仍正常的 Dashboard、竞争解释与区分实验。

## Reverse Reconstruction

症状：随机测试高、部署到新机构后失败。

从结果反推至少四条 Broken Edge 假设路径。每条路径必须包含：

```text
possible broken relation
  → predicted secondary symptom
  → discriminating evidence
  → result that would weaken the hypothesis
```

## Pass 3 · Transfer

选择 Agent、医疗或投资研究：

1. 保留机制结构；
2. 重新定义节点现实含义；
3. 指出不能直接迁移的 Edge；
4. 注入一个领域特有 Failure；
5. 建立 Unknown Register。

## Pass 4 · Open-book Repair

对照 Chapters 1–8，但不要把自己的图替换成标准图。Revision Log 记录：

- Missing Node；
- Unsupported Edge；
- Wrong Direction；
- Missing Boundary；
- Better Alternative Map；
- Remaining Unknown。

## Passing Standard

- 不依赖章节顺序也能恢复核心关系；
- 每条关键 Edge 有 Claim、Boundary 与 Evidence；
- 能正向预测 Failure，也能从症状反推假设；
- Transfer 保留机制而非替换术语；
- 允许合理替代结构，并明确 Unknown。

