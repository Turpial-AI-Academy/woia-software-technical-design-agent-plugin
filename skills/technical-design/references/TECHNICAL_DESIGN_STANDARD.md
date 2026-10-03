# Technical Design Standard

## Objective

Technical design turns established architecture into stable implementation contracts that multiple components, integrations, or future changes need to share.

It answers:

> Given these architectural boundaries, what technical contracts must be true so implementation can proceed consistently without every SPEC re-deciding cross-boundary semantics?

It does not attempt to document every implementation detail.

## Boundary with adjacent concerns

| Concern | Owns |
|---|---|
| Requirements/product | desired behavior, user/business outcomes, acceptance intent |
| Architecture | system structure, major boundaries, dependency direction, durable structural decisions |
| Technical design | concrete cross-boundary responsibilities, contracts, data/interaction semantics, ownership, failure/consistency/compatibility rules |
| Development conventions | repository-wide ways of coding, naming, formatting, local verification, contribution practice |
| SPEC | behavior and acceptance criteria for one concrete change |
| Tasks | ordered implementation work for a SPEC |
| Testing | testing strategy, coverage/risk model, test implementation policy |
| Security | threat/risk analysis and security control assurance |
| Observability | telemetry/operations detection policy |
| Deployment | promotion and deployment procedure |

Technical design may reference constraints from adjacent concerns but must not silently take ownership of them.

## Core principles

### 1. Evidence before design

Inspect actual code, schemas, integrations, documentation, and consumers. A diagram or architecture document states intent; implementation evidence shows what currently exists.

### 2. Preserve architecture boundaries

Technical design may expose that architecture is insufficient or contradictory. When that happens, stop and surface an architecture decision instead of hiding a boundary change inside detailed design.

### 3. Prefer the minimum stable contract

Document a contract when at least one of these is true:

- multiple components or repositories must agree on it;
- multiple SPECS are likely to rely on the same semantics;
- an external integration requires stable behavior;
- persistence or state semantics must survive implementation changes;
- failures/retries/concurrency can create correctness risk;
- compatibility or migration requires an explicit invariant.

Do not document local helper signatures merely because they exist.

### 4. Name authority and ownership

For shared state or behavior, state:

- authoritative source or system of record;
- contract owner;
- producers/writers;
- consumers/readers;
- allowed mutation path;
- reconciliation or migration owner when applicable.

Avoid “shared” surfaces with no owner.

### 5. Define semantics, not only shapes

A schema alone is incomplete when consumers need to know what values mean.

Define, where material:

- required/optional/null/empty semantics;
- invariants and state transitions;
- ordering or uniqueness;
- success and error meanings;
- partial/unknown outcomes;
- compatibility/versioning expectations.

### 6. Add distributed/concurrency mechanisms only when justified

Do not automatically prescribe transactions, queues, idempotency, OCC, locks, retries, or sagas.

When a real risk exists, make the required property explicit first, then choose the smallest mechanism that establishes it.

### 7. Separate current state from proposal

Use clear language:

- **Observed/current**: verified in repository/runtime evidence.
- **Documented intent**: stated by existing design/ADR/docs.
- **Proposed/recommended**: new design not yet implemented.
- **Unknown/open**: requires a decision or evidence.

Never present a recommendation as already implemented.

### 8. Make later SPECS simpler

A useful technical design centralizes shared rules so a SPEC can reference them. It should not pre-write every future SPEC.

## Minimum useful deliverable

A proportionate technical-design document normally includes:

1. scope and evidence;
2. architecture boundaries preserved;
3. responsibility/ownership map;
4. cross-cutting contract catalog;
5. interaction/data/state flows where needed;
6. failure/consistency/concurrency semantics where needed;
7. compatibility/migration constraints where needed;
8. implementation constraints that multiple changes must preserve;
9. validation evidence;
10. open decisions and explicit SPEC handoff.

Small systems may combine sections. Complex systems may split them into schemas/ADRs/contracts while keeping one index.

## Amendments and evidence lifecycle

Amend the affected explanation or traceability entry of a healthy existing contract record when real API/schema/persistence, ownership, state, failure, concurrency and compatibility semantics are unchanged. Confirm the relevant implementation/consumer evidence, preserve unrelated contracts/artifacts and valid proof, and revalidate the changed clarity plus mandatory owner/boundary/semantic/SPEC-separation invariants. Do not replay the whole design template or catalog.

Separate reusable evidence with provenance/scope from invalidated evidence and dependent claims, fresh observations/executed checks, and assumptions/inferences. A relevant source/semantic mutation or failed invariant invalidates affected proof. New/uncertain designs or real contract, data/migration, failure/concurrency, security or deployment changes require the deep path and relevant validators. Unknown external outcomes need reconciliation: NO RESPONSE != NO EFFECT remains true on every path.

## Completion gate

Technical design is sufficient when:

- later implementation can identify the owner and semantics of every material shared contract;
- cross-boundary data and interaction behavior is not left to contradictory local guesses;
- architecture is preserved or explicitly escalated for decision;
- failure/concurrency/compatibility behavior is explicit where correctness depends on it;
- current versus proposed state is distinguishable;
- change-specific acceptance criteria and task decomposition remain outside technical design;
- unresolved questions are visible and routed to the correct owner.

More pages are not evidence of a better design.
