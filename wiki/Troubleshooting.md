# Troubleshooting

This page covers cross-platform symptoms. Use the owning library Wiki for detailed domain-specific diagnostics.

## A library resolves an older ESPressio dependency

Inspect the complete PlatformIO dependency graph. The 1.0.0 baseline should not be mixed with historical pre-1.0 generations. A single downstream package can otherwise pull an older Observable, Threads, Timing or Serializable generation.

## RTTI-related build errors

Do not enable RTTI merely to restore an obsolete Observable/Event routing pattern. The 1.0.0 Observable typed registry and Event `EventTypeKey` model are designed without RTTI-based dispatch.

Check that the application is using current 1.0.0 headers/APIs rather than historical examples.

## Provider-dependent objects use the wrong allocator/clock/runtime

Install the target providers before constructing long-lived objects that capture provider/allocator state. Some allocators intentionally retain the provider that existed when they were constructed.

## ESP32 runs out of internal heap despite free PSRAM

Not all memory can move to PSRAM. Native WiFi/ESP-NOW, RTOS task stacks, driver queues, DMA/ISR-capable resources and task-control structures may require internal-capable memory.

Profile largest free internal block as well as total free heap. Use System `ExternalPreferred` only for suitable ESPressio-owned storage.

## Event or Thread worker drops/rejects work

Inspect bounded queue capacities and peak occupancy. Do not solve overload by changing to unbounded storage. Tune capacity, worker cadence and producer rate, and surface rejection telemetry.

## State consumer misses intermediate values

That may be correct. State is latest-truth semantics and can coalesce/supersede revisions. If every transition must be observed, model the information as Event instead.

## Command accepted but result arrives later

Asynchronous routed Commands can distinguish acceptance from completion. Ensure the caller requested the appropriate response expectation and that the transport response route/pending-request capacity is configured correctly.

## ESP-NOW fails during WiFi scan or transition

When WiFi coordinates the shared radio, temporary `RadioUnavailable` is expected during scans/mode transitions. Do not bypass the coordinator; retry according to the higher-level protocol semantics after reconciliation completes.

## ESP-NOW channel/interface mismatch

When WiFi owns the radio, use channel `0` and `Auto` peer interface unless the application deliberately requires an explicit channel/interface. Infrastructure STA association determines the effective physical channel.

## WiFi callbacks deadlock when calling WiFi again

Current WiFi callbacks are designed to execute after internal manager locks are released. If a custom provider/integration invokes application callbacks while holding its own locks, correct that extension rather than adding re-entry workarounds at the call site.

## Observable throws an ownership/lifetime error

Notification-capable Observable instances have explicit lifetime requirements. Do not convert required shared ownership into direct/stack ownership simply to remove a heap allocation.

## Persisted configuration cannot be decrypted or deserialized

Distinguish Security/authentication failure from Serializable schema/deserialization failure and storage failure. Protected persistence deliberately keeps these result layers separate.

## Serial diagnostics expose too much or destabilize timing

Reduce verbosity and keep diagnostic parsing/output bounded. Never print credentials/keys/protected material. Defer expensive formatting away from timing-sensitive synchronous callbacks where possible.

## Still unclear?

Identify the owning semantic domain first—System, Threads, Timing, Event, Command, State, WiFi, etc.—then use that library's Wiki rather than debugging through the transport or platform layer first.