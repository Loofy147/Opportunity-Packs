# Verification and Release Policy

## Evidence states

- **ESTABLISHED**: directly supported by inspected source or a reproducible check.
- **EXPERIMENTALLY_SUPPORTED**: passed in the named test environment and scope.
- **NOT_RUN**: the required execution has not occurred.
- **UNKNOWN**: behavior or contract is not established by the available source.
- **CONTRADICTED**: direct evidence disproves the claim.

Never promote a result from schema validation to runtime correctness. A mock context does not prove Opscotch runtime semantics, networking, persistence durability, processor lifecycle, or acknowledgement propagation.

## Required release gates

1. JSON parsing and inventory integrity pass.
2. Every pack's workflow and bootstrap pass the current Opscotch schema validators.
3. Every processor passes syntax parsing and local regression tests.
4. The official Opscotch test runner executes every discoverable `*.test.json` fixture against a compatible agent; capture the runtime version and test output.
5. Replace all example endpoints and ephemeral trust keys; prove outbound permissions are least-privilege.
6. Verify replay, partial acknowledgements, connection failure, timeout, malformed response, restart and checkpoint behavior.
7. Review secrets, licensing, ownership, support, rollback and observability before production.

Until gate 4 is backed by retained runtime evidence, the release state must remain a candidate and the runtime status must remain `NOT_RUN`.

## Security defaults

- Never commit secrets or private signing keys.
- Treat public keys as trusted configuration; never leave all-zero or test keys in production examples.
- Use explicit outbound host/method/path allow-lists.
- Bound input bytes, item counts, and page sizes before expensive parsing or fan-out.
- Delivery is at-least-once unless the receiver supplies durable idempotency; do not claim exactly-once delivery.
- Advance polling cursors only after verifying acknowledgement of the exact batch identifier and unique-item count.
