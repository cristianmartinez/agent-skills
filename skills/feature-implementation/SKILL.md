---
name: feature-implementation
description: Implement an approved feature in coherent, verified slices while preserving its product and architecture contracts. Use when outcomes and ownership are settled and the user asks to build, implement, or complete the feature; routes discovery, planning, assessment, and isolated bug diagnosis to their own workflows.
license: MIT
---

# Feature Implementation

Deliver the approved feature as working repository changes. Preserve the intended outcome and architecture while adapting implementation details to evidence discovered in the codebase.

The unit of progress is a **coherent slice**: behavior integrated far enough to prove something real. Disconnected scaffolding, unused abstractions, types without behavior, and placeholder TODOs are not completed slices.

## 1. Establish the implementation contract

Extract from the request, product definition, architecture decision, issue, and repository:

```text
Outcomes      Observable behavior the feature must deliver
Scope         First slice, non-goals, and explicit exclusions
Architecture  Owners, interfaces, invariants, flows, and migration decisions
Proof         Acceptance examples, tests, measurements, or review evidence
Constraints   Compatibility, security, performance, rollout, and repository rules
```

Reuse available information. Resolve low-cost implementation details from repository evidence and ask only when a missing product judgment or authorization would materially change the result.

If no formal architecture exists, inspect the system and make local implementation decisions that preserve current ownership and interfaces. Establish an explicit architecture decision before editing when the feature requires a new source of truth, cross-module invariant, public contract, or migration strategy.

This step is complete when each in-scope outcome has a plausible owner and a way to prove it.

## 2. Reconcile the design with the repository

Before editing:

- Read governing instructions and public build and test entry points.
- Inspect current status and preserve user changes.
- Trace the representative path the feature extends or replaces.
- Locate owning modules, interfaces, tests, persistence, and external contracts.
- Check that architecture assumptions match the current code.

Maintain a compact implementation ledger:

```text
Outcome | Owner/interface | Required change | Proof | Status
```

Record decisions that affect the next action. Repository behavior is the source of truth for implementation status; plans describe intent, not completed code.

## 3. Choose coherent slices

Order work by dependency and learning value. Prefer an early slice that exercises the real path and can reject a wrong design.

A useful slice crosses the necessary layers for one behavior—such as contract, domain logic, persistence, adapter, and user entry point—without attempting the entire feature at once. Infrastructure-only work is a valid slice when it independently proves a risky capability.

For migrations or contract changes, choose an explicit compatibility sequence such as expand → migrate → switch → contract. Name the condition that permits removal of temporary paths.

Before each slice, establish:

- Behavior added or changed
- Invariant and owner
- Behavior that must remain unchanged
- Focused proof that closes the slice

## 4. Scale execution

Classify each slice—not only the feature—as **mechanical**, **bounded**, **integrative**, or **architectural/high-risk** using ambiguity, coupling, blast radius, reversibility, novelty, and verification clarity. Handle a narrow feature as one execution unit.

For a substantial feature, a multi-agent request, or an environment where model routing or parallel execution is being considered, read [references/delegation.md](references/delegation.md) before dispatching work. The coordinator retains shared contracts, integration, and final proof.

## 5. Implement and prove each slice

For each slice:

1. Establish a failing or discriminating signal when practicable. Prefer an acceptance-level example at the owning interface, with narrower tests where they improve diagnosis.
2. Make the smallest coherent change that satisfies the contract. Reuse and deepen existing modules before introducing parallel abstractions.
3. Integrate every required path for the slice. Produce live behavior with justified seams and one source of truth.
4. Run the focused proof. Correct failures before widening scope.
5. Refactor only what is required for a clear, maintainable implementation and remove temporary diagnostics introduced for this task.
6. Update the ledger from observed results.

Keep feedback tight: search before broad reading, run focused checks before full suites, and summarize repeated output. Token and tool efficiency must not replace integration or verification.

## 6. Handle design drift explicitly

Classify new evidence before continuing:

- **Implementation detail:** Product outcome and architecture remain intact. Decide locally and continue.
- **Local design adjustment:** An owning module's internal shape changes without altering its interface or source of truth. Record it and continue.
- **Architecture contradiction:** Ownership, public interface, source of truth, identity, or migration strategy must change. Stop the affected slice and present the evidence, impact, and recommended correction before proceeding.
- **Product ambiguity:** Alternatives create meaningfully different user behavior. Ask for the missing judgment.
- **Unrelated defect:** Keep it outside the feature unless it blocks implementation or the user expands scope. Report it with evidence.

Fit the implementation to current evidence, not a stale plan. Preserve approved product meaning unless the user changes it.

## 7. Close integration gaps

Trace every outcome through its full path and check applicable concerns:

- Authorization, validation, privacy, abuse, and failure recovery
- Loading, empty, error, cancellation, retry, and accessibility behavior
- Persistence, concurrency, idempotency, compatibility, and migration
- External contracts, configuration, observability, and operational ownership
- Documentation or examples that define how users and maintainers use the feature
- Retirement of superseded paths after their migration gate is satisfied

Apply relevant checks to find missing integration, not to expand the product definition.

## 8. Verify at increasing scope

Run checks in the cheapest order that isolates failures:

1. Focused proof for each coherent slice
2. Tests for affected interfaces and neighboring behavior
3. Static analysis, formatting, build, and repository-required checks
4. Broader regression suites when blast radius or policy justifies them
5. Manual or visual verification when automation cannot establish behavior
6. An independent acceptance or integration pass for substantial features when delegation is available

A feature is complete when:

- Every in-scope outcome is implemented and demonstrated
- Architecture decisions and repository conventions are preserved or explicitly revised
- Relevant failure and recovery paths behave intentionally
- Required migrations and compatibility paths have verified gates and ownership
- Tests reject the most likely incorrect implementations
- Cross-slice integration is verified from the combined state
- No task-created temporary diagnostics or unused scaffolding remains; the feature introduces no unexplained fallback or duplicate source of truth
- Residual risk and unverified behavior are stated precisely

Do not deploy, publish, merge, commit, or mutate external systems unless the user requested or separately authorized that action.

## Final response

Keep the handoff decision-oriented:

```text
Delivered: <user-visible outcomes>
Design: <important ownership or implementation decisions>
Proof: <focused, integration, and broader verification>
Changed: <reviewable file or module summary>
Residual: <known risk, deferred scope, or “none known”>
```

Include commands and file references only when they help the user review, reproduce, or continue the work.
