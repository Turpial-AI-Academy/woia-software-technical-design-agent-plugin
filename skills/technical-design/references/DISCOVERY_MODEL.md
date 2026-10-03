# Technical Design Discovery Model

## Goal

Build enough evidence to materialize architecture into contracts without inventing a parallel system model.

## Evidence layers

Inspect the smallest relevant subset of:

### Intent

- architecture documents and diagrams;
- ADRs and design notes;
- requirements and product constraints;
- existing technical-design or interface documentation.

### Implementation

- module/package/service boundaries;
- entry points and call sites;
- APIs, RPCs, events/messages, files, schemas, generated clients/types;
- persistence models, migrations, constraints, indexes, stored procedures;
- integration adapters and protocol boundaries;
- state machines and workflows.

### Behavioral evidence

- contract/integration tests;
- fixtures showing accepted/rejected payloads;
- error/result handling in consumers;
- transaction, retry, timeout, locking/OCC, idempotency, deduplication, and reconciliation code;
- migration/compatibility behavior.

### Operational evidence

Use only when it changes the technical contract:

- deployment/runtime topology;
- process boundaries;
- external service guarantees;
- latency/size/rate limits;
- availability assumptions.

## Contract evidence record

For each material surface, record:

~~~text
name:
boundary:
current source:
owner/authority:
producer(s):
consumer(s):
shape/protocol:
invariants:
failure semantics:
consistency/concurrency:
compatibility:
evidence:
status: observed | documented-intent | proposed | unknown
~~~

Omit fields that are genuinely irrelevant; do not fill them with invented policy.

## Contradictions

Common contradictions include:

- docs name one authority while code writes another;
- schema permits values consumers cannot handle;
- producer returns error states consumers collapse into “not found”;
- architecture says one-way dependency while implementation imports backward;
- retry exists without idempotency for a non-repeatable mutation;
- multiple consumers interpret null/empty/unknown differently;
- migrations change a shared field without an explicit compatibility path.

Record the contradiction before designing the fix.

## Discovery stop condition

Discovery is sufficient when you can identify:

- which boundaries participate;
- which contracts cross those boundaries;
- who owns each contract/state;
- which semantics are already established;
- which unknowns are material to a safe shared design.

Do not delay design merely to inventory unrelated repository surfaces.
