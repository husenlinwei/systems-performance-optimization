# Learning Resources

This list is intentionally narrow. The goal is to build a machine-level performance intuition, not to collect every computer science book.

## Core Path

1. C language, memory, pointers, and data layout.
2. Assembly basics for the target architecture.
3. Operating system concepts: processes, threads, virtual memory, syscalls, scheduling, filesystems.
4. Linux kernel source, read by subsystem and problem rather than linearly.
5. CPU architecture and quantitative analysis.
6. Vendor optimization manuals for the target CPU.
7. Papers, patents, and production source code for the mechanism being studied.
8. Statistical physics or information theory when studying energy, entropy, limits, and distribution-driven behavior.

## Books and Manuals

- `Inside the C++ Object Model`
- `Linux kernel` source code
- Linux kernel scenario or internals books, especially those that explain real execution paths
- `Computer Architecture: A Quantitative Approach`
- `Intel 64 and IA-32 Architectures Optimization Reference Manual`
- Operating system internals books for the specific OS being studied
- Database systems papers and source code for storage, concurrency, logging, and query execution
- Statistical thermodynamics or statistical physics introductions for energy/information intuition

## Source Code to Study

- libc memory and string functions
- Linux kernel locking, scheduler, memory-management, and networking paths
- high-performance queues, allocators, loggers, parsers, and serializers
- database storage engines, WAL implementations, buffer pools, and transaction managers
- network stacks and RPC frameworks under realistic load

## Paper Topics

- cache replacement and locality
- transactional memory
- NUMA-aware synchronization
- lock algorithms and queueing locks
- log-structured storage
- query optimization
- consensus and replication performance
- memory allocators
- tail latency in large-scale services

## Practice Projects

- Write a microbenchmark comparing copy, zero-copy, and streaming designs.
- Compare lock, sharded lock, single-writer queue, and process-based isolation under contention.
- Measure sequential versus random memory access at different working-set sizes.
- Implement a small append-only log and measure fsync, batching, and recovery costs.
- Profile a parser or serializer, then remove one allocation or copy from the hot path.
- Compute CPI or equivalent performance counters for a small workload and explain the bottleneck.

## Study Rule

Do not read advanced material as trivia. Attach every reading session to a concrete question:

- Why is this operation slow?
- What physical or architectural limit appears here?
- What state or data movement creates the cost?
- How would I measure this?
- How would I avoid the cost in a real system?
