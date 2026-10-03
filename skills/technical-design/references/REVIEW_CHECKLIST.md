# Technical Design Review Checklist

Use proportionally. “N/A” is valid when justified.

A healthy explanation amendment checks the affected contract entry and mandatory architecture/ownership/semantic invariants; preserve unchanged contracts and valid evidence rather than replaying every item. Record reused, invalidated and freshly observed/executed evidence separately from assumptions. Real API/schema/persistence/state/failure/concurrency/security changes or missing durable proof require the deep path; relevant schema/client/contract checks and unknown-outcome reconciliation remain required.

## Evidence and scope

- [ ] Relevant architecture/boundaries were inspected.
- [ ] Current/observed behavior is separated from proposed design.
- [ ] Contradictions and unknowns are visible.
- [ ] The design scope excludes unrelated repository cleanup or architecture redesign.

## Contract quality

- [ ] Each material shared contract has an owner or authority.
- [ ] Producers/writers and consumers/readers are identifiable.
- [ ] Shape/protocol and semantic meaning are both clear enough for consumers.
- [ ] Required/optional/null/empty/sentinel behavior is explicit where ambiguous.
- [ ] State transitions/invariants are explicit where correctness depends on them.
- [ ] Error/result variants preserve distinctions callers need.
- [ ] Compatibility/versioning is defined when versions or persisted data can coexist.

## Interaction correctness

- [ ] Ordering is documented where reordering changes correctness.
- [ ] Durable commit/authority point is clear for multi-step interactions.
- [ ] Retry behavior is defined only where retries can occur.
- [ ] Idempotency/deduplication is present when duplicate effects are a real risk.
- [ ] Concurrent-write behavior is defined when stale overwrite is a real risk.
- [ ] Unknown external outcomes are not treated as proven non-effects.
- [ ] Reconciliation/compensation exists where partial effects require it.

## Boundaries

- [ ] Technical design preserves architecture or explicitly escalates an architecture decision.
- [ ] No arbitrary coding-style policy was introduced.
- [ ] No test/security/observability/deployment policy was taken over.
- [ ] Change-specific acceptance criteria and task decomposition remain in SPECS/tasks.
- [ ] The design contains no speculative abstraction justified only by hypothetical future reuse.

## Validation and handoff

- [ ] Real schemas/contracts/types/tests were checked when available.
- [ ] Later SPECS can reference shared contracts without re-defining them.
- [ ] Proposed but unimplemented behavior is labeled as such.
- [ ] Open decisions have an owner or destination.
- [ ] Executed checks and blocked/skipped checks are reported accurately.
