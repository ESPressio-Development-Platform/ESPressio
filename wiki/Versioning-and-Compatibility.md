# Versioning and Compatibility

The coordinated documentation baseline described by this Wiki is **ESPressio 1.0.0**.

## One coherent platform baseline

All ESPressio libraries documented here should be treated as members of the same 1.0.0 generation. Do not infer compatibility from historical pre-1.0 release numbers or use those old version labels as guidance for current APIs.

## Source of truth

The 1.0.0 Wiki is derived from the current coordinated working-branch architecture used to prepare the baseline. Historical README/changelog entries may describe earlier generations and are not authoritative for the new baseline where they conflict with the 1.0.0 documentation.

## Public semantic contracts

Compatibility includes more than function signatures. It also includes:

- ownership/lifecycle requirements;
- synchronous versus asynchronous behaviour;
- transport/wire framing where a protocol declares stability;
- State revision/ACK semantics;
- Command request/response semantics;
- memory/provider capability expectations;
- thread-safety and callback lock boundaries;
- persisted schema/wire representations where documented.

## Optional integrations

Optional integration headers should preserve core independence. Adding an integration may add a dependency, but the base library should not acquire that dependency merely because the integration exists.

## Provider compatibility

A platform provider is compatible when it satisfies the semantic contract, not merely when it compiles against the interface. Capability reporting, failure behaviour, ownership, interrupt safety and lifecycle must match the documented expectations.

## Wire and persisted data

Where a library exposes a wire/persistence contract, version/schema changes should be deliberate and migration-aware. Local implementation changes such as removing RTTI must not silently alter stable external identifiers or payload framing unless the protocol version is intentionally advanced.

## Breaking changes after 1.0.0

After the baseline is released, incompatible public API/semantic changes should require an appropriate major-version change. Minor/patch changes should preserve the documented 1.x compatibility contract.

## Documentation policy

The Wiki should be updated alongside active development so release documentation reflects the code that is actually intended to ship, rather than reconstructing the architecture after release.