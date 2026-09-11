---
name: solution-architecture
description: Map a defined product or feature onto an existing software system and produce an evidence-backed technical design before execution planning. Use when deciding where behavior belongs, what to reuse or introduce, how data and control cross modules, which existing paths must change, or whether a proposal needs architectural work. Do not use for early product discovery, task breakdown, or implementation.
license: MIT
---

# Solution Architecture

Turn approved product intent into a technical design grounded in the system that must support it. Decide what owns the behavior, which interfaces and invariants change, what can be reused, and what must be proven before implementation.

The output is an architecture decision, not an implementation plan. Stop before task decomposition or code changes unless the user explicitly starts a separate phase.

## 1. Establish the feature contract

Begin with the available product definition, specification, issue, or conversation. Extract:

```text
Problem      The user or business problem being solved
Actors       Who initiates, experiences, or administers the behavior
Outcomes     Observable behavior that must become true
First slice  The smallest product-complete scope under consideration
Constraints  Security, privacy, compatibility, performance, operational, or policy limits
Non-goals    Behavior deliberately outside this design
```

Preserve product decisions as constraints on the architecture. Label unresolved product questions instead of silently answering them for technical convenience. If the contract is too ambiguous to determine ownership or behavior, ask only for the consequential missing judgment; otherwise proceed with explicit assumptions.

This step is complete when the required behavior and design constraints can be evaluated independently of a proposed implementation.

## 2. Read the current system

For an existing repository, inspect the smallest sufficient set of evidence:

- Governing architecture, domain, and operational documentation
- Relevant entry points, data flows, state transitions, modules, and interfaces
- Tests that express current behavior and invariants
- Persistence formats, external contracts, configuration, and deployment boundaries when affected
- Recent changes and repository status when they alter the interpretation of current behavior

Trace at least one representative path end to end. Distinguish confirmed repository facts from architectural inference. Do not treat folder names, diagrams, planned documents, or type definitions alone as proof of runtime ownership.

For a greenfield system, replace repository evidence with confirmed platform, team, integration, and lifecycle constraints. Keep unproven choices explicit.

This step is complete when the current owner, source of truth, relevant interfaces, and failure behavior are known—or specifically recorded as missing.

## 3. Map product concepts to technical ownership

For every material product concept or operation, identify:

- The module that should own its invariant
- The interface callers need and what it guarantees
- The source of truth and identity model
- Inputs, outputs, state transitions, errors, retries, and cancellation
- Persistence and external-system crossings
- The seam through which behavior can vary or be tested

Prefer one authoritative owner for each rule and state transition. Interfaces include everything callers must know: contracts, ordering, errors, configuration, and performance expectations—not only function signatures.

Expose ownership gaps, duplicated truth, caller-enforced conventions, circular knowledge, and behavior guessed by presentation or host layers. Treat existing behavior as part of the architecture: say which paths remain, adapt, migrate, deprecate, or disappear.

This step is complete when every in-scope outcome has an owner and a traceable path through the system.

## 4. Decide what changes

Classify each required capability:

- **Reuse:** An existing primitive already owns the required semantics.
- **Deepen:** The correct module exists, but its interface or guarantees must expand.
- **Introduce:** No existing owner can coherently enforce the new invariant; add a primitive at a justified seam.
- **Replace or remove:** An existing path would otherwise duplicate ownership, preserve conflicting semantics, or become a fallback implementation.
- **Defer:** The capability is outside the first slice and the architecture remains viable without pretending it exists.

Prefer the least extensive design that fully supports the feature contract. Avoid new abstractions based only on imagined variation. A new seam earns its cost when real callers, adapters, lifecycle differences, or test needs require behavior to vary there.

Architecture is not a directory inventory. Describe responsibilities, interfaces, invariants, and flows before suggesting file placement.

## 5. Compare real options

Generate alternatives only when a consequential decision is genuinely open. Compare two or three viable approaches using the same criteria:

- Product-contract fit
- Ownership and source-of-truth clarity
- Complexity exposed to callers
- Reuse and leverage across current needs
- Migration, compatibility, and reversibility
- Testability and observability
- Security, privacy, performance, and operational consequences
- New failure modes and long-term change cost

Reject an option with a concrete reason. Do not include a knowingly weak alternative merely to create the appearance of choice.

Recommend one direction. State which evidence supports it, which tradeoff it accepts, and what new information would reverse the decision.

## 6. Convert uncertainty into proofs

For each material unknown, define the cheapest observation that can resolve it before or during implementation:

- Focused test or contract check
- Prototype or spike
- Trace of a representative flow
- Data-shape or migration sample
- Benchmark under a named workload
- Security or failure-mode review
- Operational measurement or rollout gate

Risks must be falsifiable. “May be slow” is not actionable; name the workload, threshold, and measurement that would change the design.

## 7. Produce the architecture decision

For substantial work, use [references/architecture-decision.md](references/architecture-decision.md). For a narrow change, compress the same reasoning into a short design note.

The design is ready for execution planning when:

- Every first-slice outcome maps to an owning module and interface
- Sources of truth, identity, and state transitions are unambiguous
- Existing paths affected by the proposal have an explicit disposition
- New primitives and seams have evidence-backed reasons to exist
- Failure, recovery, compatibility, migration, and operational behavior are addressed where relevant
- Material uncertainty has a proof checkpoint or an explicit deferral consequence
- The recommendation preserves the product contract without relying on a hidden fallback or duplicate implementation

End with an execution handoff containing architectural sequence and gates, not a file-by-file task list. Keep unresolved product decisions separate from technical unknowns.
