---
name: solution-architecture
description: Map a defined product or feature onto an existing software system and produce an evidence-backed technical design before execution planning. Use when deciding where behavior belongs, what to reuse or introduce, how data and control cross modules, which existing paths must change, or whether a proposal needs architectural work. Do not use for early product discovery, task breakdown, or implementation.
license: MIT
---

# Solution Architecture

Turn approved product intent into a technical design grounded in the system that must support it. Decide what owns the behavior, which interfaces and invariants change, what can be reused, and what must be proven before implementation.

The output is an architecture decision, not an implementation plan. Do not decompose tasks or change code within this phase. After architectural confirmation, continue only when the user's requested scope includes the next phase.

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

For substantial or cross-cutting work, use delegation strategically when the environment supports it. When routing is supported and authorized, the strongest permitted reasoning model coordinates the feature contract, ownership decisions, and synthesis. Independent bounded roles may trace the current flow, inventory reusable primitives and callers, or challenge failure, migration, and operational assumptions. Parallelize only disjoint read-only discovery; do not use agent consensus as architectural evidence. Without routing, use the current permitted model for these roles. For narrow work or environments without delegation, perform them locally.

## 3. Resolve the architecture decision frontier

After gathering repository evidence, expose only the consequential decisions that remain. Do not make the user answer repository facts the agent can determine. Ask for judgments that change ownership, contracts, risk posture, compatibility, or long-term cost.

Work in short proposition-led rounds. Each question must include the evidence, a concrete recommendation, its consequence, and the lowest-friction answer form that preserves the decision:

```text
Y / N / ?       Accept, reject, or explore a recommendation
A / B / C       Choose genuinely categorical designs
1–5             Choose a position on a named tradeoff
free text       Add constraints, corrections, examples, or alternatives
```

Accept compact answers, prose, partial answers, and notes such as “do not forget offline recovery.” Maintain an architecture decision ledger:

```text
confirmed | rejected | unresolved | inferred | superseded
```

When an answer corrects the product definition, mark affected architecture branches stale and return the correction to the definition contract before continuing. When the user answers `?`, explain the viable options and recommend one. Proceed on a reversible inference only when uncertainty, consequence, correction cost, and propagation breadth are low.

## 4. Map product concepts to technical ownership

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

## 5. Decide what changes

Classify each required capability:

- **Reuse:** An existing primitive already owns the required semantics.
- **Deepen:** The correct module exists, but its interface or guarantees must expand.
- **Introduce:** No existing owner can coherently enforce the new invariant; add a primitive at a justified seam.
- **Replace or remove:** An existing path would otherwise duplicate ownership, preserve conflicting semantics, or become a fallback implementation.
- **Defer:** The capability is outside the first slice and the architecture remains viable without pretending it exists.

Prefer the least extensive design that fully supports the feature contract. Avoid new abstractions based only on imagined variation. A new seam earns its cost when real callers, adapters, lifecycle differences, or test needs require behavior to vary there.

Architecture is not a directory inventory. Describe responsibilities, interfaces, invariants, and flows before suggesting file placement.

## 6. Compare real options

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

## 7. Convert uncertainty into proofs

For each material unknown, define the cheapest observation that can resolve it before or during implementation:

- Focused test or contract check
- Prototype or spike
- Trace of a representative flow
- Data-shape or migration sample
- Benchmark under a named workload
- Security or failure-mode review
- Operational measurement or rollout gate

Risks must be falsifiable. “May be slow” is not actionable; name the workload, threshold, and measurement that would change the design.

## 8. Produce the architecture decision

For substantial work, use [references/architecture-decision.md](references/architecture-decision.md). For a narrow change, compress the same reasoning into a short design note.

The design is ready for execution planning when:

- Every first-slice outcome maps to an owning module and interface
- Sources of truth, identity, and state transitions are unambiguous
- Existing paths affected by the proposal have an explicit disposition
- New primitives and seams have evidence-backed reasons to exist
- Failure, recovery, compatibility, migration, and operational behavior are addressed where relevant
- Material uncertainty has a proof checkpoint or an explicit deferral consequence
- The recommendation preserves the product contract without relying on a hidden fallback or duplicate implementation
- The user has confirmed consequential architectural judgments, or each unresolved judgment is explicitly deferred with its consequence

Use the strongest permitted reasoning capability for final synthesis. A skill cannot silently change the user's selected model or authorize extra cost. End with a planning handoff containing architectural sequence, interfaces, invariants, proof gates, migration constraints, unresolved decisions, and decision status, provenance, and dependencies—not a file-by-file task list. Reference an existing lifecycle ledger rather than maintaining a conflicting copy. Keep unresolved product decisions separate from technical unknowns.
