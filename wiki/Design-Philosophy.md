# Design Philosophy

ESPressio is built around a small set of architectural principles that should remain visible in both public APIs and internal implementation choices.

## Explicit domain ownership

Each library owns one coherent problem domain. Command expresses requested work, Event expresses something that happened, State expresses current truth, WiFi owns WiFi lifecycle, Persistence owns storage semantics, and so on.

Avoid convenience features that duplicate another library's authority.

## Dependency inversion

Higher-level libraries depend on portable abstractions rather than platform SDKs. System and other domain contracts sit above target implementations.

## Optional composition

Integrations should be opt-in. Adding ESPressio Serial should not force every subsystem monitor into the build; using local Events should not require Serializable; ordinary Persistence should not force Security.

## Deterministic embedded resource use

Prefer bounded queues, fixed capacities where practical, explicit worker cadence and stable failure modes over unbounded desktop-style growth.

Memory optimisation is valuable only when lifecycle, thread-safety and ownership semantics remain correct.

## Explicit ownership and lifecycle

RAII handles, release policies, provider lifetime and shared ownership requirements are part of the API contract, not implementation trivia.

Do not replace explicit lifecycle with hidden background ownership simply to make call sites shorter.

## Synchronous versus asynchronous semantics

Observable is synchronous. Event is asynchronous. Task/Threads provide execution boundaries. A library should not silently change a synchronous operation into asynchronous work or vice versa without making that semantic explicit.

## Typed contracts

Prefer compiler-checked types over stringly-typed routing and undocumented numeric conventions. Units, TypedEvent/State definitions, Command values and Serializable schemas all follow this principle.

## Portable public APIs

Native ESP-IDF/Arduino/FreeRTOS types should not leak through platform-neutral domains. Native details remain implementation concerns below provider/adaptor boundaries.

## Fail visibly

Unsupported capability, capacity exhaustion, malformed input, authentication failure and radio unavailability should be distinguishable rather than collapsed into silent fallback wherever the contract can expose them usefully.

## Source of truth

The 1.0.0 Wikis document the coordinated current architecture. Historical APIs and compatibility paths should not dominate new developer guidance.