# AI Glossary

| Term | 中文 | 一句话解释 | First appearance |
|---|---|---|---|
| Mental Model | 心智模型 | 用来组织概念、关系和因果结构的内部地图 | Prelude |
| Machine Learning | 机器学习 | 让系统从数据和反馈中形成可用于新输入的规则 | Prelude |
| Objective Function | 目标函数 | 把系统希望优化的结果写成可比较的数学目标 | Prelude |
| Scaling Laws | 规模定律 | 描述模型性能如何随模型规模、数据量和计算量系统变化的经验规律 | Prelude |
| Representation Learning | 表示学习 | 让模型从数据中学习适合任务的内部表示 | Prelude |
| Interpretability | 可解释性 | 研究模型内部机制及其输出原因能否被人理解和验证 | Prelude |
| AI Alignment | AI 对齐 | 研究 AI 系统的行为与人类真实意图和长期目标是否一致 | Prelude |
| Alpha Generation | Alpha 生成 | 从信息和结构变化中形成具有超额收益潜力的可检验信号 | Prelude |
| Portfolio Optimization | 组合优化 | 在收益、风险、相关性、容量与成本约束下分配投资权重 | Prelude |
| Online Learning | 在线学习 | 随新数据持续到来而更新模型或信念的学习方式 | Prelude |
| Familiarity | 熟悉感 | 再次看到材料时产生的识别感，但不保证能够主动回忆或使用 | Chapter 01 |
| Recall | 回忆 | 在没有原材料提示时取回事实、步骤或公式的能力 | Chapter 01 |
| Understanding | 理解 | 能够解释、预测、重建并迁移一个关系模型的能力 | Chapter 01 |
| Transfer | 迁移 | 把已学关系用于不同输入、任务或领域的能力 | Chapter 01 |
| Rule Compression | 规则压缩 | 用较少关系表示多个观察中共享的结构 | Chapter 01 |
| Inductive Bias | 归纳偏置 | 在有限数据支持多种解释时，学习系统偏好某类规则的假设 | Chapter 01 |
| Perturbation Test | 扰动测试 | 主动改变一个条件并在运行前预测后果，以检验因果理解 | Chapter 01 |
| Driver Tree | 驱动因素树 | 把结果拆分为可分析、可预测和可证伪的底层驱动关系 | Chapter 01 |
| Grokking | 顿悟式泛化 | 模型在训练集早已拟合后，测试泛化于更晚训练阶段显著出现的现象 | Chapter 01 |
| Local Rule | 局部规则 | 系统中的一个部分根据有限邻域或接口信息执行的更新关系 | Chapter 02 |
| Iteration | 迭代 | 把一次更新的结果作为下一次输入并反复执行的过程 | Chapter 02 |
| Interaction | 交互 | 一个部分的状态或输出影响其他部分后续行为的连接关系 | Chapter 02 |
| State | 状态 | 系统在某一时刻保留、并会影响下一步的信息 | Chapter 02 |
| Emergence | 涌现 | 未被直接写入单个局部规则、却由局部交互生成的全局可观察结构 | Chapter 02 |
| Cellular Automaton | 元胞自动机 | 在离散网格上反复应用局部更新规则的动态系统 | Chapter 02 |
| Function Composition | 函数组合 | 把一个函数的输出作为另一个函数的输入以形成更复杂变换 | Chapter 02 |
| Feedback Loop | 反馈回路 | 系统输出返回并影响后续输入、状态或行为的循环关系 | Chapter 02 |
| Synchronous Update | 同步更新 | 所有部分读取同一旧状态并同时产生下一状态的更新方式 | Chapter 02 |
| Abstraction | 抽象 | 围绕任务保留必要关系、隐藏可替换细节并声明边界的契约 | Chapter 03 |
| Interface | 接口 | 使用者观察或操作系统的边界，而无需依赖全部内部实现 | Chapter 03 |
| Invariant | 不变量 | 内部实现改变时仍必须保持成立的关系或承诺 | Chapter 03 |
| Equivalence Class | 等价类 | 在某个抽象和任务下被视为相同的一组具体状态 | Chapter 03 |
| Abstraction Leakage | 抽象泄漏 | 被隐藏的实现细节穿过接口并迫使调用者依赖内部结构 | Chapter 03 |
| Representation | 表示 | 把观察编码成可计算形式，并由此定义系统可见的差异、几何与操作 | Chapter 04 |
| Observation | 观察 | 现实通过传感器、记录或采样进入系统的部分 | Chapter 04 |
| Encoding | 编码 | 把观察写成符号、类别、数字或其他结构的规则 | Chapter 04 |
| Representation Geometry | 表示几何 | 一个表示赋予对象的距离、邻近与方向关系 | Chapter 04 |
| Representation Collision | 表示碰撞 | 两个任务相关的不同观察被编码成同一表示 | Chapter 04 |
| One-hot Encoding | 独热编码 | 用一个激活位置和其余零位置区分离散类别的表示方法 | Chapter 04 |
| Cyclical Encoding | 周期编码 | 把周期变量映射到圆上以保留首尾邻近关系的表示方法 | Chapter 04 |
| Vector | 向量 | 对象在多维属性空间中的表示 | Chapter 11 |
| Matrix | 矩阵 | 描述空间或表示如何变化的规则 | Chapter 12 |
| Linear Transformation | 线性变换 | 用结构化、可组合的方式把一种表示变成另一种表示 | Chapter 13 |
| Nonlinearity | 非线性 | 打破纯线性限制，使模型表达复杂规律 | Chapter 14 |
| Activation Function | 激活函数 | 把非线性引入神经网络的函数 | Chapter 14 |
| ReLU | 线性整流单元 | 让正信号通过、把非正信号截断为零的激活函数 | Chapter 14 |
| Gradient | 梯度 | 告诉参数局部最有效改进方向的信号 | Chapter 15 |
| Loss Function | 损失函数 | 把模型预测与目标之间的差距变成可优化的数字 | Chapter 16 |
| Cross Entropy | 交叉熵 | 衡量模型给正确类别分配的概率是否足够高 | Chapter 16 |
| Mean Squared Error | 均方误差 | 用平方误差衡量数值预测偏离目标的程度 | Chapter 16 |
| Optimization | 优化 | 使用梯度和更新策略逐步降低目标函数的过程 | Chapter 17 |
| Learning Rate | 学习率 | 控制每次参数更新步幅大小的超参数 | Chapter 17 |
| Stochastic Gradient Descent | 随机梯度下降 | 用小批量样本估计梯度并更新参数的优化方法 | Chapter 17 |
| Momentum | 动量 | 让优化器利用过去更新方向以减少震荡和加速下降的机制 | Chapter 17 |
| Adam | Adam 优化器 | 结合动量和自适应步幅的常用深度学习优化器 | Chapter 17 |
