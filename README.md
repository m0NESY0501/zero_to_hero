## 项目：复现 Karpathy 的 micrograd

这是我复现并学习 Andrej Karpathy 的教程《building micrograd》的实现，代码以 Jupyter Notebook 的形式保存在 `micrograd.ipynb` 中。该工程的目的是手工实现一个极简的自动微分引擎（reverse-mode autodiff），并用它搭建一个小型神经网络（MLP）以理解反向传播的原理。

主要工作（高层概述）

- 实现了核心数据结构 `Value`：封装标量值、追踪计算子节点、储存梯度并支持反向传播（`backward()`）。
- 实现了算子重载：支持加、减、乘、除、幂、tanh、exp 等运算，并为每个运算定义了反向传播函数。
- 实现了计算图可视化：使用 `graphviz` 绘制计算图，便于展示前向计算与梯度流。
- 构建了神经网络模块：`Neuron`、`Layer`、`MLP`，支持把 `Value` 组成的小网络作为前向模型并进行参数优化。
- 实现了训练循环：手写均方差损失、梯度清零、反向传播、参数更新（简单的 SGD），并演示收敛行为。
- 与 PyTorch 的小示例对比：计算结果与 PyTorch 的 `tanh` 自动微分一致，方便验证正确性。

关键文件

- `micrograd.ipynb`：完整的 Notebook，包括 `Value` 类定义、计算图绘制函数、示例（单个神经元/MLP）以及训练循环。该文件为本仓库的主要展示内容。

如何运行（快速指南）

1. 建议在虚拟环境中运行（Python 3.8+）：创建并激活环境后安装依赖。

   - 主要依赖：
     - graphviz（用于渲染计算图；注意：需同时安装系统层面的 Graphviz，可在 <https://graphviz.org/> 下载）
     - matplotlib、numpy
     - （可选）torch 用于对比实验

2. 安装示例（在 Windows PowerShell）：

```
pip install graphviz matplotlib numpy
# 可选：
pip install torch
```

1. 在 Jupyter 中打开并运行 `micrograd.ipynb`：

- 打开终端（PowerShell），进入项目目录 `d:\CS_Projects\zero to hero`，运行 `jupyter notebook` 或 `jupyter lab`，然后在浏览器中打开 `micrograd.ipynb`。
- Notebook 中包含多个演示单元：
  - 基本的 `Value` 与操作符实现
  - 使用 `draw_dot()` 绘制计算图（需要系统安装 Graphviz）
  - 与 PyTorch 的对比示例
  - 一个小型 MLP 的训练循环示例

演示要点（建议在展示时强调）

- 如何通过最小的代码实现反向传播（可读性强、易于教学）。
- 计算图可视化如何帮助理解链式法则和梯度流向。
- 与 PyTorch 的对比验证：即使是这样一个极简实现，也能得到与主流框架一致的梯度结果。

扩展与下一步（可选）

- 增加更多激活函数与损失函数的实现；
- 支持向量化操作以提升效率；
- 添加更完善的训练监控（loss 曲线可视化）和单元测试。

参考

- Andrej Karpathy, "micrograd" 教程与源码（强烈建议阅读原文以获得直观讲解）。

如果你需要，我可以：

- 把 Notebook 中的某些关键图（比如计算图、训练曲线）导出为图片并放入仓库；
- 补充一份更详尽的中文讲解文档，适合放在 PPT 或报告中展示。

----
文件位置：`micrograd.ipynb`
这是我跟随 Karpathy 的教程实现的自动微分引擎，旨在深入理解反向传播和计算图。
