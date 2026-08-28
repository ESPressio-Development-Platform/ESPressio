# Getting Started

ESPressio is designed to be consumed as a set of focused libraries rather than one monolithic framework.

Start by choosing the domain abstractions your application actually needs, then add the target/platform provider that implements the required hardware/runtime contracts.

## Typical ESP32 composition

A substantial ESP32 application might use:

```text
System + platform providers
        |
        +--> Task / Threads
        +--> Timing
        +--> Observable
        +--> Serializable
        +--> Event / Command / State
        +--> Persistence / Security
        +--> WiFi / ESP-Now
        +--> Serial diagnostics
```

Not every application needs every layer.

## Foundation first

Understand these concepts before building higher-level integrations:

- [System memory/provider model](https://github.com/ESPressio-Development-Platform/ESPressio-System/wiki/Home)
- [Observable synchronous notification](https://github.com/ESPressio-Development-Platform/ESPressio-Observable/wiki/Home)
- [Serializable declarative schemas](https://github.com/ESPressio-Development-Platform/ESPressio-Serializable/wiki/Home)
- [Threads lifecycle model](https://github.com/ESPressio-Development-Platform/ESPressio-Threads/wiki/Home)

## Choose the correct communication primitive

- Use **Command** for requested work and execution results.
- Use **Event** for facts/transitions that happened and may need asynchronous fan-out.
- Use **State** for the latest truth where obsolete intermediate revisions are disposable.
- Use **Observable** for synchronous in-process lifecycle notification.

See [Communication Model](Communication-Model).

## Install providers early

Platform providers such as memory, clocks, execution and GPIO should be installed before constructing long-lived objects that capture those providers or allocator state.

On ESP32 this target composition belongs in the ESPressio-ESP32/platform layer rather than in portable domain libraries.

## Keep optional dependencies optional

Select integrations explicitly. A local Event should not require Serializable; a console/logger should not pull in Command/Event/Security; WiFi should not pull in Persistence unless configuration storage is selected.

## Next

Read [Architecture](Architecture), [PlatformIO and Installation](PlatformIO-and-Installation) and the Wiki for each library you plan to consume.