# Performance Checklists

## Triage Checklist

- What changed recently?
- Which metric regressed: average latency, p95, p99, throughput, CPU, memory, cost, error rate, queue depth?
- Is the regression global or tied to a route, tenant, query, payload, hardware class, region, or traffic shape?
- Is the bottleneck CPU-bound, memory-bound, IO-bound, network-bound, lock-bound, database-bound, or scheduler-bound?
- Is there a profile, trace, query plan, counter, or reproducible benchmark?
- Does load increase linearly, superlinearly, or hit a hard plateau?
- Does adding workers help, do nothing, or make things worse?

## Architecture Review Checklist

- Does the hot path copy large payloads?
- Is data serialized and deserialized multiple times inside one request?
- Are services split in a way that creates avoidable network round trips?
- Does a central coordinator, global lock, singleton, queue, or database row serialize work?
- Are writes and reads contending on the same data structure or storage path?
- Can work be partitioned by key, shard, core, tenant, symbol, account, or time window?
- Can immutable snapshots, append-only logs, or single-writer ownership simplify concurrency?
- Are indexes, materialized views, caches, and denormalization solving the actual workload?
- Is backpressure explicit, or does the system hide overload with retries and queues?

## Code Review Checklist

- Are allocations visible in the hot path?
- Are loops doing repeated length checks, parsing, lookups, formatting, logging, or conversions?
- Are data structures chosen for locality and access pattern, not only API convenience?
- Are hash maps, regex, JSON, reflection, dynamic dispatch, or exceptions used in tight loops?
- Is the common case separated from the rare case?
- Are branch conditions stable and predictable?
- Is memory access mostly sequential?
- Are buffers reused safely?
- Are locks held across IO, logging, allocation, callbacks, or network calls?
- Is error handling cheap in the success path?

## Database Checklist

- Inspect the query plan before changing code.
- Check cardinality estimates, index usage, join order, sort/hash operations, temp files, and row counts.
- Look for N+1 queries, over-fetching, repeated queries, unbounded scans, and chatty transactions.
- Check transaction duration, lock waits, isolation level, write amplification, and hot rows.
- Prefer schema and access-pattern fixes over sprinkling caches blindly.
- If caching is proposed, state the key, value, TTL or invalidation rule, consistency model, and memory budget.

## Concurrency Checklist

- Measure contention, not only CPU.
- Look for global locks, atomic hot counters, shared queues, false sharing, cache-line bouncing, and NUMA effects.
- Estimate the serial fraction. If it is non-trivial, adding cores has a hard ceiling.
- Prefer ownership partitioning and local aggregation.
- Use lock-free or spin-based techniques only when blocking cost is proven dominant and correctness can be kept simple.
- For user-space systems, avoid open-ended spinning under oversubscription.

## Optimization Proposal Template

Use this compact template when reporting a plan:

```text
Target:
Current evidence:
Dominant cost:
Why this cost exists:
Avoid-cost option:
Reduce-cost option:
Verification:
Risks:
Rollback:
```

## Benchmark Checklist

- Run the old and new versions under the same workload.
- Include realistic input sizes and distributions.
- Report variance and tail behavior.
- Avoid measuring only warm cache or only ideal alignment unless that is the production case.
- Separate benchmark harness overhead from the operation.
- Confirm whole-system impact after microbenchmark improvement.
