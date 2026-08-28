# Core Concepts

This page is the platform-level map of ESPressio concepts. Follow the linked library Wikis for complete usage and extension guidance.

## System and memory

[ESPressio System](https://github.com/ESPressio-Development-Platform/ESPressio-System/wiki/Home) defines portable execution, synchronization, queues, clocks, GPIO and memory placement. `MemoryPolicy` lets ESPressio-owned storage express `Automatic`, `Internal`, `ExternalPreferred` or `ExternalRequired` intent without exposing target allocation APIs.

## Task and Threads

[Task](https://github.com/ESPressio-Development-Platform/ESPressio-Task/wiki/Home) owns bounded execution primitives and task-runtime creation. [Threads](https://github.com/ESPressio-Development-Platform/ESPressio-Threads/wiki/Home) owns long-lived lifecycle-managed workers, precision scheduling, registry/cleanup and Thread-level observability.

Use Task for bounded units of work; use Threads for persistent worker identity/lifecycle.

## Observable

[Observable](https://github.com/ESPressio-Development-Platform/ESPressio-Observable/wiki/Home) is synchronous one-to-many notification. Typed observer interfaces are bound at registration time without RTTI-based dispatch.

## Event

[Event](https://github.com/ESPressio-Development-Platform/ESPressio-Event/wiki/Home) is asynchronous typed fan-out. Events represent things that happened and may need independent consumers.

## Command

[Command](https://github.com/ESPressio-Development-Platform/ESPressio-Command/wiki/Home) represents intent: something should be done. It provides typed parameters, validation, synchronous/local invocation and request/response routing for asynchronous transports.

## State

[State](https://github.com/ESPressio-Development-Platform/ESPressio-State/wiki/Home) represents current truth. Newer revisions supersede obsolete pending ones; State deliberately does not preserve every intermediate transition.

## Serializable

[Serializable](https://github.com/ESPressio-Development-Platform/ESPressio-Serializable/wiki/Home) lets a type declare one authoritative schema independent of JSON, CBOR, ESPB Binary, streaming or persistence destination.

## Units

[Units](https://github.com/ESPressio-Development-Platform/ESPressio-Units/wiki/Home) makes physical meaning and magnitude part of the C++ type system.

## Timing and clocks

[Timing](https://github.com/ESPressio-Development-Platform/ESPressio-Timing/wiki/Home) owns clocks, stopwatches, deadline scheduling and distributed clock discipline above System's primitive clock providers.

## Persistence

[Persistence](https://github.com/ESPressio-Development-Platform/ESPressio-Persistence/wiki/Home) separates file/key-value storage semantics from concrete platform backends. Serializable and protected persistence are optional layers above the raw storage contracts.

## Security

[Security](https://github.com/ESPressio-Development-Platform/ESPressio-Security/wiki/Home) owns data-protection, key, entropy and transport-security abstractions. Cryptographic policy remains separate from storage and serialization policy.

## WiFi and ESP-Now

[WiFi](https://github.com/ESPressio-Development-Platform/ESPressio-WiFi/wiki/Home) owns WiFi lifecycle and is the authority for the ESP32 shared radio when conventional WiFi and ESP-NOW coexist. [ESP-Now](https://github.com/ESPressio-Development-Platform/ESPressio-ESP-Now/wiki/Home) owns ESP-NOW transport/topology and follows WiFi's radio state.

## Serial

[Serial](https://github.com/ESPressio-Development-Platform/ESPressio-Serial/wiki/Home) is the downstream operator/diagnostics layer. It consumes System byte I/O and authoritative public APIs from monitored domains.