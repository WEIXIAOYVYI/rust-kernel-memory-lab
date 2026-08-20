# Rust Kernel Memory Lab

这是一个关于 Rust 内核内存管理（Memory Management, MM）的学习、设计与实验仓库。

目标不是简单复刻 Linux MM，而是通过：

- 问题建模（Problem Modeling）
- 最小模型（Minimal Model）
- 不变量设计（Invariant）
- Rust 所有权模型（Ownership / Lifetime）
- Linux / xv6 / Rust OS 对比
- 原型验证与实验

逐步形成一套适合 Rust Kernel 的 MM 设计方法。

## 核心理念

> 先理解问题，再设计机制；先定义 invariant，再写代码。

## 仓库定位

本仓库记录：

- MM 学习过程
- 设计决策
- 架构权衡
- 实验结果
- 失败尝试和反思

最终目标：

设计一个现代 Rust Kernel Memory Management Subsystem。

