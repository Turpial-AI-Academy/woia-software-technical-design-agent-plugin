# Interaction and Failure Model

## Start from the correctness property

Before selecting a mechanism, state what must remain true.

Examples:

- one logical operation must not create duplicate effects;
- stale clients must not overwrite newer state;
- a projection may lag but must never grant access from an unverified snapshot;
- a caller must distinguish “absent” from “response invalid”;
- a lost response must not cause a non-repeatable mutation to be executed blindly again.

Then choose the smallest mechanism that establishes the property.

## Sequencing

Document ordering only when reordering can change correctness.

A useful sequence records:

~~~text
initiator
-> validation/context
-> authoritative read
-> mutation/effect
-> durable result
-> audit/event/projection
-> response
~~~

The real sequence may differ. Mark which step is the durable commit point.

## Transactions

Use a transaction when multiple writes must succeed/fail as one correctness unit and the datastore supports the required boundary.

Do not use “transactional” as a synonym for “safe”.

Clarify:

- transaction scope;
- isolation/conflict behavior when relevant;
- external effects that cannot participate;
- reconciliation when local commit and external effect can diverge.

## Idempotency and deduplication

Use when the same logical operation may be delivered or submitted more than once and duplicate effects are harmful.

Define:

- idempotency/deduplication key;
- key scope and lifetime;
- canonical stored result;
- behavior for repeated matching requests;
- behavior for reused keys with conflicting payloads.

A retry loop alone does not create idempotency.

## Optimistic concurrency / version checks

Use when stale readers can overwrite newer state.

Define:

- version/etag/expected state;
- conflict result;
- client behavior after conflict;
- operations that intentionally bypass OCC, if any.

Do not require OCC when concurrent overwrite is impossible or harmless.

## Retries

For a retryable operation, define:

- which failures are retryable;
- attempt/backoff limits when they are part of the contract;
- whether the operation is safe to repeat;
- which identifier remains stable across attempts;
- terminal behavior after exhaustion.

Never prescribe automatic retry for every error.

## Unknown outcomes

A timeout, connection loss, missing response, or missing log can leave mutation state unknown.

Unless the external contract proves otherwise:

~~~text
NO RESPONSE != NO EFFECT
~~~

For a material unknown outcome, choose an explicit behavior such as:

- query by stable operation identifier;
- reconcile from authoritative state;
- return a pending/unknown result;
- require operator review for irreversible effects.

Do not blindly replay a non-idempotent operation merely because the response was lost.

## Eventual consistency and projections

When derived state can lag:

- identify the authority and the projection;
- define acceptable freshness/staleness;
- state which decisions may use stale data;
- define reconciliation;
- prevent a stale projection from becoming an accidental new authority.

## Error semantics

Errors should be distinguishable when callers must react differently.

In particular, preserve distinctions such as:

- authoritative absence vs invalid/corrupt response;
- rejected input vs conflict with current state;
- forbidden vs unavailable;
- known failure vs unknown outcome.

Do not introduce a universal error taxonomy if the repository already has a healthy one.

## Human-visible design evidence

For high-impact interactions, a sequence table is often enough:

| Step | Actor | Input/state | Action | Durable effect | Failure/unknown behavior |
|---|---|---|---|---|---|

Use diagrams only when they clarify behavior more effectively than text.
