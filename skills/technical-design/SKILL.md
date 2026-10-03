---
name: technical-design
description: Translates established software architecture into implementation-ready cross-cutting technical contracts. Use when defining component responsibilities, APIs/interfaces, schemas, data ownership, interaction flows, state transitions, consistency, concurrency, retries, idempotency, failure semantics, compatibility, or a reusable technical-design document without duplicating change-specific SPEC detail.
license: MIT
compatibility: Works with software repositories across languages and architecture styles; the agent needs access to the relevant architecture and repository evidence, and repository-specific tooling only when validating concrete contracts.
metadata:
  author: Turpial AI Academy
  version: "0.5.0"
---

# technical-design

## Operating flow

~~~text
DISCOVER -> DECIDE -> IMPLEMENT -> VALIDATE -> REPORT
~~~

## Purpose

Translate established architecture into the minimum stable technical contracts needed to implement and evolve a system without crossing healthy boundaries or forcing later SPECS to rediscover shared semantics.

## Non-negotiable rules

- Discover before designing.
- Treat architecture as an input constraint. Do not silently redesign system boundaries while claiming to produce technical design.
- Model observed/current behavior separately from proposed/recommended behavior.
- Design stable cross-cutting contracts, not every local function or class.
- Give each material shared contract an owner or authority and identify producers/consumers.
- Preserve healthy existing contracts and naming unless evidence justifies change.
- Add retries, idempotency, OCC, transactions, queues, caching, versioning, or other mechanisms only when the actual failure/concurrency/compatibility model requires them.
- Never infer that a timeout, missing response, or missing log proves an external mutation did not occur.
- Keep change-specific behavior, acceptance criteria, edge cases, and implementation steps in SPECS/tasks rather than duplicating them here.
- Keep technical design distinct from coding-style policy, test strategy, security review, observability policy, and deployment procedure.
- Do not report skipped validation as passed.

## Minimum-sufficient evidence

Choose depth from the affected shared contract and evidence health. A new turn does not require rediscovering unchanged design.

### Bounded amendment

Use the fast path for a local explanation or traceability clarification in a healthy existing contract record when actual APIs/interfaces, schemas, persisted formats, ownership, state transitions, failure semantics, concurrency and compatibility behavior remain unchanged.

1. Locate the authoritative technical-design record and the affected contract entry or explanation.
2. Inspect only the relevant producer/consumer, schema, or behavioral evidence needed to confirm agreed semantics still match implementation. Documentation establishes intent; prose or recollection alone is not execution proof.
3. Amend the smallest affected section in place. Preserve unrelated contracts, architecture decisions, design artifacts and valid evidence; do not replay the full contract catalog or technical-design template.
4. Revalidate affected clarity plus mandatory invariants: owner/authority and producers/consumers are clear, architecture boundaries are preserved, material data/failure/concurrency semantics remain coherent, and change-specific detail stays in SPECS/tasks.
5. Report reused evidence with source identity/scope, invalidated evidence and dependent claims, fresh observations/executed checks and results, and assumptions/inferences separately. Missing responses never establish non-effects.

### Deep path and evidence invalidation

Use the deep path for a new design/contract, unclear scope, contradictory or missing durable evidence, or an actual API/schema/event, persisted data/migration, ownership, state-transition, failure, concurrency, compatibility, auth/security, integration or deployment/rollback change. An architecture-boundary change must be escalated explicitly. Trace affected producers/consumers and required cross-cutting invariants; preserve healthy unrelated design.

Reuse evidence only while its contract/source identity, producers/consumers, data/state/failure/concurrency semantics, target environment and validation conditions remain covered. A relevant mutation or failed invariant invalidates affected proof and dependent claims; freshly inspect the changed semantics and execute required schema/client/contract checks. Assumptions remain unverified. Unknown external mutation outcomes require authoritative reconciliation; preserve NO RESPONSE != NO EFFECT and never blindly replay a non-idempotent effect.

Load references by trigger: standard/discovery for new, unhealthy or ambiguous design; contract catalog for a contract-category/semantic decision; interaction/failure model for ordering, state, retries, concurrency or unknown outcomes; SPEC boundary for ownership of change-specific detail; review checklist for affected invariants or a full design gate. Templates support missing artifacts or necessary restructuring, not recreation of a healthy record.

## Discover

For new or materially uncertain design work, read [TECHNICAL_DESIGN_STANDARD.md](references/TECHNICAL_DESIGN_STANDARD.md) and [DISCOVERY_MODEL.md](references/DISCOVERY_MODEL.md) before making design-policy decisions. A bounded clarification starts with the existing record and relevant contract evidence.

Inspect, as applicable:

- architecture documents, ADRs, diagrams, requirements, and existing technical-design documents;
- modules, packages, services, processes, entry points, public interfaces, schemas, events/messages, files, and persistent models;
- callers/consumers and implementations/producers of shared contracts;
- databases, caches, queues, object stores, external APIs, identity boundaries, and integration adapters;
- existing error envelopes, state machines, transactions, locks/OCC/version fields, idempotency keys, retries, deduplication, and reconciliation behavior;
- compatibility promises, migrations, generated clients/types, and legacy consumers;
- tests only as evidence of established contract semantics, without taking over test-policy ownership.

Build an evidence-backed map:

~~~text
architecture boundary
  -> responsibility
  -> contract
  -> authority/owner
  -> producers/consumers
  -> state/data flow
  -> failure/consistency semantics
  -> compatibility constraints
~~~

Record contradictions and unknowns before proposing a target contract.

## Decide

Use [CONTRACT_CATALOG.md](references/CONTRACT_CATALOG.md) for shared contract semantics, [INTERACTION_AND_FAILURE_MODEL.md](references/INTERACTION_AND_FAILURE_MODEL.md) when interaction/failure correctness is involved, and [SPEC_BOUNDARY.md](references/SPEC_BOUNDARY.md) when detail ownership is uncertain.

For each candidate contract:

1. identify the architectural boundary or repeated cross-cutting need it serves;
2. state current evidence and whether the contract already exists;
3. define its owner/authority and consumers;
4. choose the smallest stable interface and semantics needed by more than one local implementation decision;
5. make data meaning, errors, state transitions, compatibility, and failure behavior explicit where material;
6. add concurrency/retry/idempotency/reconciliation mechanisms only when justified by real risk;
7. mark unresolved product- or change-specific questions for SPECS instead of guessing;
8. reject abstractions whose only justification is future reuse or stylistic uniformity.

## Implement

A technical-design task usually changes documentation, schemas/contracts, or design assets rather than application code.

Common outcomes include:

- create or update a repository technical-design document;
- define a cross-boundary API, event, message, file, or persistence contract;
- document source-of-truth and ownership rules;
- formalize an error/result envelope or state-transition model;
- document interaction ordering and what must happen on partial/uncertain failure;
- define compatibility/versioning constraints for multiple consumers;
- clarify transactional, idempotency, deduplication, OCC, locking, or reconciliation semantics where needed;
- identify which details must be deferred to individual SPECS.

Amend a healthy existing record in place. Use [technical-design.template.md](assets/technical-design.template.md) and [contract-catalog.template.md](assets/contract-catalog.template.md) for new or structurally incomplete artifacts, not mandatory bureaucracy.

## Validate

Use [REVIEW_CHECKLIST.md](references/REVIEW_CHECKLIST.md) for affected invariants or a full gate; a bounded clarification applies relevant checks plus mandatory contract/boundary invariants.

Validation should establish, as applicable:

- every material contract maps to an established boundary or justified shared need;
- owner/authority and producers/consumers are unambiguous;
- data fields and special values have defined meaning where ambiguity would affect consumers;
- error/failure states are distinguishable enough for callers to act correctly;
- retries and concurrent operations cannot silently duplicate or overwrite effects when such risk exists;
- compatibility/migration constraints are explicit when multiple versions or consumers coexist;
- proposed design does not contradict architecture without an explicit architecture decision;
- later SPECS can reference the shared contract without copying cross-cutting semantics;
- the design document does not contain task breakdowns or change-specific acceptance criteria disguised as technical design.

When real schemas, generated clients, tests, or validators exist, run the repository-specific checks that prove the contract remains coherent.

## Report

Report:

1. evidence inspected and current-state facts;
2. architecture boundaries assumed/preserved;
3. contracts created, clarified, preserved, or intentionally deferred;
4. owner/authority and producer/consumer relationships;
5. interaction, data, failure, consistency, concurrency, and compatibility decisions that materially apply;
6. proposed versus already-implemented behavior;
7. validation actually executed and results;
8. unresolved questions that belong to product/architecture/SPECS;
9. remaining risks and migration notes.

For amendments, identify the changed record, preserved contracts, reused/invalidated/fresh evidence, and unresolved assumptions.

Keep facts, proposals, and unresolved assumptions visibly distinct.

## Detailed references

- [Technical Design Standard](references/TECHNICAL_DESIGN_STANDARD.md)
- [Discovery Model](references/DISCOVERY_MODEL.md)
- [Contract Catalog](references/CONTRACT_CATALOG.md)
- [Interaction and Failure Model](references/INTERACTION_AND_FAILURE_MODEL.md)
- [SPEC Boundary](references/SPEC_BOUNDARY.md)
- [Review Checklist](references/REVIEW_CHECKLIST.md)
