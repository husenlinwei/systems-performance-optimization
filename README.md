# Systems Performance Optimization Skill

Chinese version: [README.zh-CN.md](README.zh-CN.md)

`systems-performance-optimization` is a Codex skill for performance diagnosis, architecture-level efficiency review, and low-level optimization planning.

It is designed for work involving latency, throughput, CPU, memory, cache behavior, concurrency, storage, networking, databases, runtimes, and systems code.

## Philosophy

The skill treats performance as the result of workload, data movement, state transitions, synchronization, and physical machine constraints.

Its default posture is:

- measure before guessing;
- understand the real workload;
- remove avoidable work before making work faster;
- prefer architecture-level prevention over local tuning;
- keep correctness and maintainability visible;
- verify changes against realistic workloads.

## Repository Layout

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

## When To Use

Use this skill when a user asks for:

- performance optimization;
- bottleneck diagnosis;
- latency or throughput improvement;
- CPU, memory, cache, lock, IO, network, or database analysis;
- architecture review for efficiency;
- a learning path for systems performance.

## What It Emphasizes

- Workload and target metrics
- Profiling, traces, query plans, counters, and reproducible benchmarks
- Data copying and serialization cost
- Lock contention and shared mutable state
- Cache locality and memory layout
- Branch predictability and hot-path simplification
- Database access patterns and transaction scope
- Whole-system verification after local improvement

## Installation

Copy or clone this folder into your Codex skills directory:

```bash
~/.codex/skills/systems-performance-optimization
```

Then invoke it explicitly:

```text
$systems-performance-optimization
```

Depending on your Codex configuration, it may also be selected automatically for relevant performance tasks.
