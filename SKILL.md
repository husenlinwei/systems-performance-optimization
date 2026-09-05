---
name: systems-performance-optimization
description: Analyze and improve system performance for latency, throughput, CPU, memory, cache, concurrency, storage, networking, databases, runtimes, and low-level code. Use when the user asks for performance optimization, bottleneck diagnosis, architecture-level efficiency review, or a learning path for systems performance.
---

# Systems Performance Optimization

Use this skill to reason about performance as a property of workload, data movement, state transitions, synchronization, and physical machine constraints. The goal is not to micro-optimize first; it is to find where the system creates avoidable cost, then remove or reduce that cost with measured evidence.

## Operating Posture

- Start from the real workload, target metric, and current evidence. If code or traces are available, inspect them before proposing changes.
- Prefer architecture-level prevention over local tuning when the bottleneck is caused by unnecessary copying, shared mutable state, synchronization, serialization, round trips, allocation churn, or poor data layout.
- Treat CPU cycles, cache misses, memory bandwidth, branch prediction, syscalls, locks, IO, network hops, and database query plans as concrete costs. Avoid explaining performance only in framework-level terms.
- Keep optimizations reversible, measurable, and scoped. Do not trade away correctness, durability, observability, or maintainability unless the user explicitly accepts the tradeoff.
- Distinguish production performance, benchmark performance, and theoretical limits. A microbenchmark can explain a mechanism, but it does not prove whole-system improvement.

## Workflow

1. Define the objective: latency percentile, throughput, CPU utilization, memory footprint, tail latency, startup time, cost, or another metric.
2. Describe the workload: data size, request shape, read/write mix, concurrency, locality, deployment topology, hardware, and hot path.
3. Gather evidence: profiles, traces, query plans, flamegraphs, counters, logs, benchmarks, or code-path inspection.
4. Classify the bottleneck: data motion, synchronization, memory hierarchy, control flow, allocation, IO, network, database, scheduler, runtime, or algorithmic complexity.
5. Ask whether the system can avoid the cost entirely before making the cost cheaper.
6. Propose the smallest change that attacks the dominant cost, plus the measurement that would confirm or reject it.
7. Verify with the same workload or a defensible reproduction, and call out residual risks.

## Decision Rules

- If copying is hot, first look for ownership, layout, batching, streaming, zero-copy, references, slices, or moving computation to the data.
- If locks are hot, first look for partitioning, single-writer ownership, queues, actor/event loops, immutable data, sharding, batching, or process isolation.
- If CPU is hot, look at instruction mix, branch predictability, cache locality, vectorization, allocations, parsing, hashing, serialization, and avoidable abstraction overhead.
- If memory is hot, look at object count, layout, locality, pooling, reuse, cache-line behavior, fragmentation, and working-set size.
- If IO or network is hot, look at round trips, batching, protocol shape, buffering, compression, backpressure, retries, and placement.
- If a database is hot, inspect query plans, indexes, cardinality, transaction scope, lock contention, data model, read/write amplification, and cache behavior.

## Supporting References

- For the full reasoning model, read [references/methodology.md](references/methodology.md).
- For code review, incident triage, or optimization planning, read [references/checklists.md](references/checklists.md).
- For study plans and source material, read [references/learning-resources.md](references/learning-resources.md).

Only load the reference that matches the current task. Keep responses grounded in the user's code, workload, and measurements whenever those are available.
