# Glossary

**Command** — A typed request that something be done, including validation and execution/result semantics.

**Event** — A typed fact that something happened, normally distributed asynchronously.

**State** — The latest authoritative truth for a typed definition/device; obsolete intermediate revisions may be superseded.

**Observable** — Synchronous in-process one-to-many notification using typed observer interfaces.

**Provider** — A concrete implementation of a platform-neutral contract, usually supplied by a target/platform package.

**MemoryPolicy** — System-level intent describing where ESPressio-owned allocations should live: Automatic, Internal, ExternalPreferred or ExternalRequired.

**ExternalPreferred** — Prefer suitable external memory while permitting the System provider's documented fallback.

**Task** — A bounded unit of execution managed through the Task runtime/executor abstractions.

**Thread** — A long-lived lifecycle-managed worker abstraction built above Task/System execution.

**PrecisionThread** — A Thread whose work is scheduled around explicit timing/iteration semantics.

**Clock discipline** — Timing's process for estimating and correcting clock phase/rate from synchronization samples.

**Slew** — Gradually applying phase correction while preserving monotonic clock progression.

**Serializable schema** — A type's authoritative declarative description of serializable members, validation and schema versioning independent of representation.

**Archive** — A Serializable representation layer such as JSON, CBOR or ESPB Binary.

**ESPB** — ESPressio's binary Serializable representation.

**StateTypeId** — Stable transport-neutral identifier for a logical State definition.

**EventTypeKey** — Compiler-backed local Event routing identity used without RTTI.

**DeviceIdentifier** — State's transport-neutral 128-bit device identity.

**Radio state** — WiFi's authoritative physical shared-radio snapshot, distinct from application-facing WiFi runtime state.

**Auto interface** — ESP-Now peer policy that follows the currently authoritative WiFi radio/interface state over the peer's lifetime.

**Bounded** — Having an explicit maximum resource capacity rather than unbounded growth.

**Snapshot** — A stable copied view used to avoid exposing mutable internal storage or holding locks across user code.

**Adapter** — A downstream integration that maps one established contract onto another without becoming a second authority for either domain.