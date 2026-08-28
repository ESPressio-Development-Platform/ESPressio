# Communication Model

ESPressio deliberately distinguishes four communication semantics that are often conflated in embedded applications.

```text
Observable  "Tell these in-process observers now."
Event       "This happened."
Command     "Please do this."
State       "This is true now."
```

Choosing the correct primitive makes transport and execution behaviour easier to reason about.

## Observable — synchronous notification

Use [Observable](https://github.com/ESPressio-Development-Platform/ESPressio-Observable/wiki/Home) when observer completion is part of the producer's operation.

```text
producer changes state
    -> notify observers synchronously
    -> return
```

Do not use Observable as a queue or ISR-to-worker transport.

## Event — asynchronous fact/history

Use [Event](https://github.com/ESPressio-Development-Platform/ESPressio-Event/wiki/Home) when something happened and independent consumers may process it asynchronously.

Events can be queued/stacked, distributed to Event-aware Threads and optionally serialized across Event Transport.

If every transition matters, Event is normally more accurate than State.

## Command — requested work

Use [Command](https://github.com/ESPressio-Development-Platform/ESPressio-Command/wiki/Home) when one component requests an operation from another.

Command provides parameter metadata/validation, typed invocation, execution results and optional asynchronous request/response routing.

Transport adapters should preserve the Command contract rather than implementing their own action grammar.

## State — latest truth

Use [State](https://github.com/ESPressio-Development-Platform/ESPressio-State/wiki/Home) when consumers care about the newest authoritative value.

```text
v10 -> v11 -> v12 -> v13

slow consumer normally needs v13
```

Pending State may be coalesced/superseded. If losing v11 or v12 would be semantically incorrect, use Event instead.

## Transport independence

Command, Event and State own domain-neutral transport contracts. Concrete transports such as ESP-NOW adapt those contracts without redefining their semantics.

For example:

```text
CommandInvocation -> ESP-NOW Command adapter -> remote Command registry
Serializable Event -> ESP-NOW Event adapter -> remote Event infrastructure
State Update       -> ESP-NOW State adapter -> remote State repository
```

## HTTP and future Web integration

HTTP/Web interfaces should adapt the same Command/Event/State authorities rather than introducing a separate application model. A synchronous HTTP request can acknowledge asynchronous work while WebSocket or Event mechanisms carry later updates where appropriate.

## Rule of thumb

Ask what the message *means* before choosing how it is transported. Transport should follow semantics, not define them.