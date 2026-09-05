# Systems Performance Methodology

## Mental Model

Performance is the result of how data and state move through a machine. Good optimization starts by making costs visible:

- data movement: copies, serialization, deserialization, memory-to-cache traffic, disk/network transfer;
- state movement: shared mutable state, coordination, invalidation, consistency, ownership transfer;
- control movement: branches, calls, virtual dispatch, interpreter/runtime transitions, syscalls;
- time movement: queueing, scheduling, retries, backpressure, lock waiting, GC pauses;
- physical limits: CPU issue width, cache hierarchy, memory bandwidth, NUMA, storage latency, network latency, power and thermal constraints.

The most valuable optimization often removes an operation instead of making the operation faster.

## First-Principles Questions

Ask these before editing code:

1. What exact workload matters?
2. What metric defines success?
3. Where does the dominant time or cost go?
4. Is the dominant cost necessary for correctness?
5. Can data stay where it is?
6. Can ownership be clearer so synchronization disappears?
7. Can the hot path do less work?
8. Can the system move from shared mutable state to local state plus messages?
9. What theoretical or practical ceiling applies?
10. What measurement would falsify the proposed fix?

## Avoid-Cost Before Reduce-Cost

Prefer this sequence:

1. Remove: eliminate copy, lock, query, allocation, parse, conversion, or round trip.
2. Reframe: change ownership, data layout, batching, topology, or algorithm.
3. Localize: keep data and state near the worker that uses them.
4. Simplify: reduce branches, modes, polymorphism, and hidden side effects in the hot path.
5. Specialize: add targeted fast paths only after measurement shows the need.
6. Micro-optimize: tune instructions, cache, vectorization, or memory barriers only for proven hotspots.

## Reading Measurements

Do not accept a single number without context. Check:

- workload representativeness;
- warmup and cache state;
- input size distribution;
- concurrency level;
- tail latency, not only average;
- CPU frequency scaling and power modes;
- allocator, GC, JIT, kernel, and filesystem effects;
- benchmark harness overhead;
- variance and confidence.

## Common Bottleneck Patterns

### Data Copying

Symptoms: high memory bandwidth, large allocation counts, serialization cost, copy functions in profiles, high GC pressure, high p99 latency under payload growth.

Questions:

- Why does this data move?
- Can producers and consumers share representation safely?
- Can the computation move to where the data already lives?
- Can streaming replace materialization?
- Can batching reduce per-item overhead?

### Synchronization

Symptoms: lock contention, blocked threads, CPU burn in spin loops, scheduler overhead, throughput flattening as cores increase, tail latency spikes.

Questions:

- Is shared mutable state required?
- Can ownership be partitioned by key, shard, core, tenant, or time window?
- Can a single writer serialize mutation while readers use immutable snapshots?
- Can queues, actors, processes, or append-only logs replace locks?
- Does Amdahl's law cap the benefit of adding cores?

### Cache and Locality

Symptoms: high LLC misses, random access, pointer chasing, large object graphs, low IPC, memory stalls, poor scaling with data size.

Questions:

- What is the working set?
- Are hot fields adjacent?
- Can arrays or struct-of-arrays replace scattered objects?
- Can cold fields move off the hot path?
- Can precomputation or indexing improve locality?

### Control Flow

Symptoms: branch misses, many small virtual calls, deep abstraction stacks, interpreter overhead, repeated parsing or validation.

Questions:

- Are branches predictable?
- Are common cases separated from uncommon cases?
- Can validation happen once at boundaries?
- Can the hot path be straight-line and mode-stable?

## Output Style for Performance Work

When answering, prefer this shape:

- objective and current evidence;
- dominant suspected cost;
- architecture-level fix if available;
- local optimization if needed;
- measurement plan;
- risks and tradeoffs.

Avoid generic advice such as "use caching" or "optimize queries" without naming what data is cached, why it is reused, and how invalidation or correctness works.
