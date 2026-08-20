# MM Design Method Card

## 七条原则

1. 从问题出发，不从 Linux 模块名出发。
2. 先建立最小模型，再研究复杂实现。
3. 先写 invariant，再写 struct。
4. Linux 是优秀参考，不是规范。
5. 每个复杂机制必须解释它解决的问题。
6. Rust 应帮助表达 ownership、lifetime 和 invariant。
7. 每轮设计都留下工程结论和学习成果。

## 固定流程

Problem
→ Minimal Model
→ Invariant
→ Ownership/Lifetime
→ Rust Model
→ Reference Comparison
→ Design
→ Test
→ Reflection
