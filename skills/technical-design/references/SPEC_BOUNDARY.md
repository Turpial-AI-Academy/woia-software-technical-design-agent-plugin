# Technical Design vs SPEC Boundary

## Durable rule

Technical design centralizes **shared technical semantics**.

A SPEC defines **one behavioral change** against those semantics.

~~~text
architecture
  -> technical design
       -> SPEC A
       -> SPEC B
       -> SPEC C
~~~

The technical-design document should make SPECS smaller, not become one giant SPEC.

## Keep in technical design

Keep a detail here when it is stable and cross-cutting, for example:

- the authoritative owner of a shared entity;
- an API/event/error envelope used by multiple changes;
- semantics of null/unknown/sentinel values consumed broadly;
- interaction ordering required across a system boundary;
- idempotency or concurrency rules every mutation of a shared resource must preserve;
- versioning/compatibility rules for multiple producers/consumers;
- a persistent state machine used by multiple features.

## Keep in a SPEC

Move a detail to the relevant SPEC when it describes one change, for example:

- user-visible behavior of a new feature;
- acceptance criteria;
- exact new fields/endpoints needed only for that change;
- edge cases specific to the change;
- migration steps introduced by that change;
- feature flag rollout for the change;
- files to edit;
- implementation sequence;
- test cases for the change.

A SPEC may extend a shared contract. When it does, the SPEC should state the change and update the canonical technical contract if the change becomes durable.

## Escalate to architecture

Return to architecture when a proposed technical design changes:

- major system boundaries;
- deployable/service split;
- dependency direction;
- ownership of a domain/responsibility;
- durable architecture style or topology;
- public contract boundary with broad system impact.

Do not smuggle architecture changes into “implementation detail”.

## Route elsewhere

Examples:

- repository-wide naming/formatting/tooling rule -> development conventions;
- coverage/test pyramid/fixture strategy -> testing;
- threat/control selection -> security;
- telemetry/SLO/alerting policy -> observability;
- environment/promotion/rollback procedure -> deployment/release capabilities.

## Review question

For every section ask:

> Will multiple implementations or future SPECS need this same semantic rule?

If yes, technical design may own it. If no, place it closer to the specific change.
