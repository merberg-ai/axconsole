# Contributing to AXConsole

AXConsole is still alpha software and touches real packet-radio transports, so changes should be small, reviewable, and regression-tested.

## Ground rules

1. Preserve daemon ownership of connected RF sessions.
2. Do not weaken TLS certificate verification, token authentication, role checks, or CIDR restrictions to make a client easier to configure.
3. Preserve protocol generation 1 compatibility unless a protocol change is explicit and documented.
4. Preserve LinPac `//COMMAND` pass-through behavior.
5. Treat the native Linux AX.25 helpers as compatibility-sensitive code.
6. Do not introduce an internal connected-mode AX.25 Layer-2 implementation as a shortcut around Linux AX.25 or Dire Wolf AGWPE.
7. Do not commit real callsign defaults, credentials, private keys, packet-history databases, session logs, or personal network configuration.

## Tests

Run the relevant test suite before submitting a change. Backend changes should include regression coverage for the behavior being changed. Client changes should preserve observer/operator permission behavior and reconnect/resume semantics.
