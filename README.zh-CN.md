# Systems Performance Optimization Skill

`systems-performance-optimization` 是一个 Codex skill，用于性能诊断、架构层效率审查和底层优化方案设计。

它适合处理延迟、吞吐、CPU、内存、缓存、并发、存储、网络、数据库、运行时和系统代码相关问题。

## 方法论

这个 skill 把性能看作 workload、数据移动、状态变化、同步机制和物理机器约束共同作用的结果。

默认工作方式是：

- 先测量，不先猜；
- 先理解真实 workload；
- 先消除不必要的工作，再让必要的工作更快；
- 优先在架构层避免问题，而不是只做局部调参；
- 始终看见正确性和可维护性；
- 用真实或可辩护的 workload 验证结果。

## 目录结构

```text
systems-performance-optimization/
|-- SKILL.md
|-- README.md
|-- README.zh-CN.md
|-- agents/
|   `-- openai.yaml
`-- references/
    |-- methodology.md
    |-- checklists.md
    `-- learning-resources.md
```

## 适用场景

当用户提出这些需求时使用：

- 性能优化；
- 瓶颈诊断；
- 延迟或吞吐提升；
- CPU、内存、缓存、锁、IO、网络或数据库分析；
- 架构效率审查；
- 系统性能学习路线。

## 重点关注

- workload 和目标指标；
- profile、trace、query plan、性能计数器和可复现 benchmark；
- 数据复制和序列化成本；
- 锁竞争和共享可变状态；
- cache locality 和内存布局；
- 分支预测和 hot path 简化；
- 数据库访问模式和事务范围；
- 局部优化后的全系统验证。

## 安装

把这个文件夹复制或 clone 到 Codex skills 目录：

```bash
~/.codex/skills/systems-performance-optimization
```

然后显式调用：

```text
$systems-performance-optimization
```

根据你的 Codex 配置，它也可能在相关性能任务中被自动选择。
