# PlatformIO and Installation

ESPressio libraries are designed to be composed explicitly through PlatformIO dependencies.

## Release baseline

For the coordinated 1.0.0 release, depend on the required ESPressio libraries at **1.0.0**. Do not mix historical pre-1.0 package generations into the same platform baseline.

A representative project might declare only the libraries it needs:

```ini
lib_deps =
    espressio-development-platform/ESPressio-System@1.0.0
    espressio-development-platform/ESPressio-Observable@1.0.0
    espressio-development-platform/ESPressio-Timing@1.0.0
    espressio-development-platform/ESPressio-Threads@1.0.0
    espressio-development-platform/ESPressio-Event@1.0.0
```

Add optional integrations only when selected.

## Target/platform package

Portable domain libraries do not contain target-native implementations of every System/WiFi/storage contract. On ESP32, the target provider package supplies the concrete implementations and adapters needed by the selected domains.

Provider initialization should occur before long-lived allocator-aware/clock/execution consumers are constructed where the platform startup model permits it.

## C++ language level

The 1.0.0 platform assumes the C++ language features required by the individual libraries and should be built with a coherent C++17-capable toolchain baseline.

Do not enable RTTI merely to compensate for an old Observable/Event usage pattern: the current Observable and Event routing models are designed around RTTI-free typed registration/identity.

## Development branches

The Wiki documents the future coordinated 1.0.0 release state. During development, the source branches used to construct this baseline may be consumed directly for integration testing, but release-facing application documentation should use `1.0.0` rather than those branch names.

## Dependency troubleshooting

When a project resolves conflicting ESPressio generations, inspect the complete PlatformIO dependency graph. One old downstream package can pull older Observable/Threads/Timing/etc. versions and invalidate the coordinated architecture.

Prefer one coherent baseline rather than individually pinning around incompatible transitive dependencies.

## Include only what you need

Many ESPressio integrations are exposed through focused headers. Avoid broad optional umbrellas when the project only requires the core domain API; this helps preserve dependency isolation and reduces compile/resource cost.