# Technical Design

## 1. Scope and status

**Purpose:**  
**Architecture source(s):**  
**Status:** observed/current | proposed | mixed  
**Out of scope:**  

## 2. Evidence

| Evidence | What it establishes | Status |
|---|---|---|
|  |  | observed / documented-intent / proposed / unknown |

For a bounded amendment, update only the affected existing contract/explanation; do not recreate a healthy design.

- Reused evidence: <source identity, contract scope, consumers and validation conditions>
- Invalidated evidence: <mutation/failed invariant and dependent claims>
- Fresh evidence: <observations/executed schema/client/contract checks and results>
- Assumptions/inferences: <unverified; not proof>

## 3. Boundaries preserved

| Boundary | Responsibility | Owner | Notes |
|---|---|---|---|
|  |  |  |  |

Architecture decisions that require escalation:

- None / ...

## 4. Contract catalog

| Contract | Boundary | Authority/owner | Producers | Consumers | Canonical form | Status |
|---|---|---|---|---|---|---|
|  |  |  |  |  |  | observed / proposed |

Use a separate schema/specification file when a machine-readable form already exists.

## 5. Data and state semantics

For each material shared data/state contract, define only what consumers need:

- identity/uniqueness;
- required/optional/null/empty/sentinel semantics;
- invariants and allowed transitions;
- authority/source of truth;
- derived/projection state;
- time/order/freshness semantics where applicable.

## 6. Interactions

| Step | Actor | Input/state | Action | Durable effect | Failure/unknown behavior |
|---|---|---|---|---|---|
|  |  |  |  |  |  |

Include only sequences where ordering matters.

## 7. Failure, consistency, and concurrency

Document as applicable:

- error/result categories;
- transactional boundary;
- retryable failures;
- idempotency/deduplication keys;
- concurrent-write/OCC/conflict behavior;
- unknown outcomes and reconciliation;
- consistency/freshness constraints.

Mark non-applicable mechanisms explicitly rather than inventing them.

## 8. Compatibility and migration constraints

- compatible producers/consumers:
- versioning rule:
- migration/rollout ordering:
- deprecation/retirement condition:

## 9. Cross-cutting implementation constraints

List only constraints multiple SPECS/implementations must preserve.

1. 
2. 

## 10. Validation

| Check/evidence | Result | Notes |
|---|---|---|
|  | PASS / FAIL / BLOCKED / NOT RUN |  |

## 11. Open decisions and SPEC handoff

### Open decisions

| Question | Owner/destination | Why it blocks or matters |
|---|---|---|
|  |  |  |

### Belongs in later SPECS

- change-specific behavior:
- acceptance criteria:
- feature-specific schema/API additions:
- implementation tasks:
