# Extension Model

ESPressio is designed to be extended by adding implementations behind stable semantic contracts rather than modifying every consumer for each new board, transport or backend.

## Platform providers

When adding a new MCU/RTOS/platform, implement the applicable System contracts for memory, execution, synchronization, queues, clocks and GPIO. Keep native SDK types below the provider boundary.

See the [System extension documentation](https://github.com/ESPressio-Development-Platform/ESPressio-System/wiki/Extension-Architecture).

## WiFi providers

A new target-specific WiFi implementation should satisfy `IWiFiPlatform`. WiFiManager keeps ownership of remembered networks, selection policy, retries, AP-until-Client semantics and radio-state publication.

See the [WiFi provider contract](https://github.com/ESPressio-Development-Platform/ESPressio-WiFi/wiki/Platform-Provider-Contract).

## Persistence backends

Implement `IFileStorage` or `IKeyValueStorage` for a new medium. Preserve capability reporting, bounded reads/writes and atomic-replacement semantics where advertised.

See [Persistence backend guidance](https://github.com/ESPressio-Development-Platform/ESPressio-Persistence/wiki/Extension-Architecture).

## Event transports

Implement Event's transport contract in the transport-owning library. Do not place WiFi/MAC/socket framing details inside Event.

See [Event Transport](https://github.com/ESPressio-Development-Platform/ESPressio-Event/wiki/Event-Transport).

## Command transports/interpreters

Add representation adapters and response routes around the authoritative Command registry. Keep transport syntax separate from Command definition/validation semantics.

See [Command extension documentation](https://github.com/ESPressio-Development-Platform/ESPressio-Command/wiki/Extension-Architecture).

## State transports/codecs

A transport carries State's update/ACK/subscription/resynchronisation protocol and maps its peer identity into `DeviceIdentifier`. Rich value types can specialize `StateCodec<TDefinition>` without introducing a mandatory serialization framework.

See [State extension guidance](https://github.com/ESPressio-Development-Platform/ESPressio-State/wiki/Extending-State).

## New Serializable representations/types

Add archives/value adapters without making model classes representation-aware. Preserve bounded decoding, detailed diagnostics and schema-evolution semantics.

See [Serializable extension documentation](https://github.com/ESPressio-Development-Platform/ESPressio-Serializable/wiki/Extension-Architecture).

## New Unit contexts

Extend Units through physical context/type metadata, conversion/formula relationships and optional Serializable counterparts while preserving dimensional safety.

See [Units extension documentation](https://github.com/ESPressio-Development-Platform/ESPressio-Units/wiki/Extension-Architecture).

## Cross-library integration rule

Place an integration in the downstream library that can legally depend on both sides. Avoid reciprocal dependencies and avoid making optional domain coupling mandatory.

## Testing extensions

Test both the semantic contract and the actual target integration. Host/unit coverage is useful, but provider, transport, radio, ISR, stack and resource-lifetime changes require representative hardware validation.