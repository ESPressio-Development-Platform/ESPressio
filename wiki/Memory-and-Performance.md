# Memory and Performance

Memory and execution cost are first-class architectural concerns across ESPressio 1.0.0.

## Memory placement is semantic

ESPressio System exposes memory policies rather than target allocators:

```text
Automatic
Internal
ExternalPreferred
ExternalRequired
```

Use them to express capability/lifetime intent for ESPressio-owned storage. Do not treat PSRAM as a universal replacement for internal memory.

## What should remain internal/native

RTOS task stacks, task-control structures, native driver queues, DMA buffers, ISR-required storage and other capability-constrained allocations must remain where the target runtime requires them.

Moving an allocation merely because external RAM exists can break correctness.

## What can often prefer external memory

Variable-size ESPressio-owned registries, snapshots, serialization buffers, listener/transport metadata and other CPU-accessed storage are candidates when their ownership/capability requirements permit it.

Examples in the 1.0.0 baseline include Observable registration storage, Event transport/listener bookkeeping, Threads manager snapshots and selected Serializable buffers.

## Avoid copies that exist only to cross a lock

The platform increasingly uses stable records, immutable shared registrations and carefully scoped snapshots so user callbacks can run after locks are released without copying whole collections or `std::function` objects on every operation.

Do not remove required snapshots if doing so would invoke user/virtual code under an internal lock.

## Bounded work

Queues, pending requests, State repositories, diagnostic traversal and transport buffers should have explicit limits. Capacity exhaustion should be observable and testable.

## Stacks

Reduce stack defaults only from measured high-water evidence on representative hardware with a retained safety margin. Compile success or a quiet unit test is not evidence that a stack is safely sized.

## Shared ownership contracts

Some objects require shared ownership for safe callback lifetime. For example, Observable notification lifetime depends on its ownership contract. Removing a `shared_ptr` allocation is not an optimisation if it invalidates that contract.

## Hardware validation

Profile the full application, not isolated libraries. Important metrics include:

- free and largest internal-capable heap block;
- external heap usage;
- worker stack high-water marks;
- queue/repository peak occupancy;
- allocation failures by native subsystems;
- timing jitter and iteration overruns;
- transport burst behaviour.

## Optimisation rule

A memory optimisation is accepted only when ownership, thread safety, lifecycle, reentrancy and platform capability guarantees remain intact.