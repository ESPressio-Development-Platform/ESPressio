# ESPressio Development Platform 1.0.0

ESPressio is a modular C++ development platform for embedded systems, designed around explicit domain boundaries, portable abstractions, event-driven composition, deterministic resource behaviour and replaceable platform providers.

The 1.0.0 baseline is documented as a coordinated platform rather than a collection of unrelated libraries.

## Documentation map

### Foundation

- [ESPressio System](https://github.com/ESPressio-Development-Platform/ESPressio-System/wiki/Home) — platform-neutral memory, execution, synchronization, queues, clocks and GPIO contracts.
- [ESPressio Units](https://github.com/ESPressio-Development-Platform/ESPressio-Units/wiki/Home) — strongly typed physical quantities.
- [ESPressio Observable](https://github.com/ESPressio-Development-Platform/ESPressio-Observable/wiki/Home) — synchronous typed observation.
- [ESPressio Serializable](https://github.com/ESPressio-Development-Platform/ESPressio-Serializable/wiki/Home) — declarative representation-neutral serialization.

### Execution and time

- [ESPressio Task](https://github.com/ESPressio-Development-Platform/ESPressio-Task/wiki/Home) — bounded task execution primitives.
- [ESPressio Threads](https://github.com/ESPressio-Development-Platform/ESPressio-Threads/wiki/Home) — long-lived managed worker lifecycle and precision scheduling.
- [ESPressio Timing](https://github.com/ESPressio-Development-Platform/ESPressio-Timing/wiki/Home) — clocks, stopwatches, scheduling and distributed clock discipline.

### Messaging and state

- [ESPressio Event](https://github.com/ESPressio-Development-Platform/ESPressio-Event/wiki/Home) — asynchronous typed Event distribution.
- [ESPressio Command](https://github.com/ESPressio-Development-Platform/ESPressio-Command/wiki/Home) — typed intent/execution and asynchronous command routing.
- [ESPressio State](https://github.com/ESPressio-Development-Platform/ESPressio-State/wiki/Home) — latest-truth distributed State.

### Persistence and security

- [ESPressio Persistence](https://github.com/ESPressio-Development-Platform/ESPressio-Persistence/wiki/Home) — portable storage contracts and typed persistence.
- [ESPressio Security](https://github.com/ESPressio-Development-Platform/ESPressio-Security/wiki/Home) — data protection, keys, entropy and transport-security contracts.

### Connectivity and operator surfaces

- [ESPressio WiFi](https://github.com/ESPressio-Development-Platform/ESPressio-WiFi/wiki/Home) — autonomous platform-neutral WiFi lifecycle.
- [ESPressio ESP-Now](https://github.com/ESPressio-Development-Platform/ESPressio-ESP-Now/wiki/Home) — ESP-NOW transport and distributed integrations.
- [ESPressio Serial](https://github.com/ESPressio-Development-Platform/ESPressio-Serial/wiki/Home) — console, logging and diagnostics.

## Start here

- [Getting Started](Getting-Started)
- [Architecture](Architecture)
- [Design Philosophy](Design-Philosophy)
- [Dependency Graph](Dependency-Graph)
- [Core Concepts](Core-Concepts)
- [Communication Model](Communication-Model)
- [Memory and Performance](Memory-and-Performance)
- [Extension Model](Extension-Model)
- [Versioning and Compatibility](Versioning-and-Compatibility)
- [Glossary](Glossary)
- [Troubleshooting](Troubleshooting)

## Scope of this baseline

This Wiki intentionally documents only the coordinated 1.0.0 platform baseline. Libraries still undergoing major architectural work or not yet implemented are omitted until they are ready to join the public platform documentation.