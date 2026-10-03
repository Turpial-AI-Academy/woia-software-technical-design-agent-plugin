# Contract Catalog

Use this catalog to decide what must be explicit. Not every project needs every category.

## 1. Responsibility contract

Defines what a component/module/service owns and what it must not own.

Minimum useful semantics:

- responsibility;
- boundary;
- owner;
- inputs/dependencies;
- outputs/capabilities;
- forbidden or intentionally excluded responsibilities.

## 2. Interface/API contract

Applies to function/module boundaries, HTTP/RPC APIs, CLI commands, plugin interfaces, or other callable surfaces used across a meaningful boundary.

Define as applicable:

- operation and intent;
- caller/consumer;
- input fields/types and requiredness;
- output/result variants;
- error categories;
- side effects;
- authorization/context expectations inherited from the system;
- compatibility/versioning.

Do not duplicate every private function signature.

## 3. Data/schema contract

Applies to persistent models, messages/events, files, payloads, generated types, or shared in-memory structures.

Define as applicable:

- authority/source of truth;
- field meaning, requiredness, null/empty/sentinel semantics;
- identity and uniqueness;
- invariants;
- timestamps/timezone/ordering;
- lifecycle/state;
- producer and consumers;
- compatibility/migration rules.

A field list without meaning is not a complete shared contract.

## 4. Integration contract

For an external service, repository, process, or system boundary, define:

- owning side and consuming side;
- protocol/transport;
- authentication/authorization assumptions already established elsewhere;
- request/response or event/file semantics;
- timeouts and external limits when contractually relevant;
- failure categories;
- retry/reconciliation expectations;
- version/compatibility ownership.

Do not turn technical design into vendor setup documentation.

## 5. Interaction/sequence contract

Use when correctness depends on ordering across boundaries.

Define:

- initiator;
- participants;
- ordered steps;
- state changes/side effects;
- commit point or authority update;
- what can be retried;
- what happens on partial or unknown outcomes;
- reconciliation/compensation where justified.

## 6. State and consistency contract

Use when multiple actors read/write shared state.

Define as applicable:

- authoritative state;
- allowed transitions;
- transactional boundary;
- consistency expectation;
- concurrent-write behavior;
- conflict detection/resolution;
- freshness/staleness rules;
- derived/projection state and reconciliation.

## 7. Error/result contract

Consumers must be able to distinguish materially different outcomes.

Possible categories include:

~~~text
success
not_found
invalid_input
conflict
forbidden
unavailable
timeout
invalid_response
unknown_outcome
~~~

Use names appropriate to the project. Do not force this exact taxonomy.

Avoid collapsing invalid/corrupt/unknown results into valid absence.

## 8. Compatibility contract

Use when producers and consumers can run different versions or persisted data outlives one deployment.

Define:

- compatible versions;
- additive/breaking change rules;
- deprecated fields/operations;
- read/write behavior during migration;
- rollout ordering constraints;
- generated client/type synchronization;
- retirement condition for compatibility bridges.

## 9. Implementation constraint

A technical-design constraint is justified when multiple changes must preserve it for correctness.

Examples:

- “writes to this state go through this owner”;
- “external mutation keys are stable across retries”;
- “consumers treat unknown outcome as pending reconciliation”;
- “older readers must tolerate this additive field”.

Local naming, formatting, directory preferences, and generic coding style belong to development conventions instead.
