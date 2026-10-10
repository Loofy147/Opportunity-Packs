# Opscotch Opportunity Packs

Reusable, constrained automation packs for Opscotch workflows.

## Status

**Current state: initial source import / stress-test candidate. Not a production release.**

This repository starts with the reviewed eight-pack candidate. Schema validity, static analysis, and local mock-context tests are not equivalent to a live Opscotch runtime test. The runtime gate stays closed until the official test runner executes each fixture against a compatible Opscotch agent.

## Packs

| Pack | Purpose | Critical boundary |
|---|---|---|
| 01 — Durable Relay | Buffer and forward events | At-least-once; receiver enforces idempotency |
| 02 — Composable Component | Reference component contract | Starter template, not a finished integration |
| 03 — Legacy Bridge | Normalize and bridge old payloads | Explicit input size caps and parsing policy |
| 04 — Signed Package Gate | Verify package signatures | Test key is never a production trust key |
| 05 — State Reconciliation | Compare expected and actual IDs | Strict input validation and bounded cardinality |
| 06 — Batch API | Reduce request overhead | Destination must honor exact batch acknowledgements |
| 07 — Cursor Poller | Poll and deliver bounded change pages | Checkpoint only after destination acknowledgement; at-least-once replay |
| 08 — Batch Transform | Normalize/deduplicate batches | Bounded input and explicit rejection behavior |

## Verification contract

Every claim must be labeled by its evidence:

- **ESTABLISHED** — directly verified from source or a reproducible test.
- **EXPERIMENTALLY_SUPPORTED** — behavior passed in an explicitly named test environment.
- **UNKNOWN / NOT_RUN** — not yet executed in the required environment.

Before production:
1. Run the official Opscotch integration test runner against a compatible agent.
2. Replace every `example.invalid` endpoint and provide explicit allow-list entries.
3. Replace the ephemeral test public key with a production trust key managed outside the repository.
4. Define a license and document any customer-specific permissions.
5. Inspect security, retry, replay, and operational recovery behavior.

## Repository policy

- Do not commit secrets or private keys.
- Do not call a pack production-ready on schema validation alone.
- Keep a deterministic local test suite, checksum validation, and a CI gate.
- Keep release artifacts reproducible from repository contents.
