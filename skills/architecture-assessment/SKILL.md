---
name: architecture-assessment
description: Reconstruct and assess the as-built architecture of a software feature, module, or system against explicit criteria, including alignment, ownership, interfaces, dependencies, state, resilience, operability, testability, and evolution. Use when the user asks whether an existing architecture is sound, aligned, scalable, maintainable, or structurally flawed. This is a read-only architecture assessment, not code review, solution design, or implementation.
license: MIT
---

# Architecture Assessment

Explain how an existing system is shaped, evaluate whether that shape serves its current responsibilities, and identify the highest-leverage improvements. Architecture quality is contextual: judge the system against its product, operational, and change pressures rather than a generic pattern catalog.

Stay read-only. Recommend direction and repair depth, but do not edit the system unless the user separately requests implementation.

## 1. Frame the assessment

Resolve:

```text
Target       Feature, module, subsystem, or whole system
Purpose      Responsibilities and outcomes the architecture must support
Question     Alignment, maintainability, scale, reliability, evolution, or broad health
Pressure     Current incidents, change costs, growth, constraints, or planned demands
Evidence     Architecture docs, ADRs, code, tests, runtime behavior, history, and metrics
```

Infer scope from the repository when practical. If the target could mean materially different systems, ask one compact scoping question. State exclusions and assumptions.

A narrow question may need a short assessment. For a broad or durable audit, use [references/architecture-assessment.md](references/architecture-assessment.md).

## 2. Establish the governing architecture

Find current product contracts, architecture documents, ADRs, repository instructions, public interfaces, data contracts, deployment topology, and operational constraints. Extract concrete claims about:

- Responsibilities and ownership
- Interfaces and permitted dependencies
- Invariants, identity, and sources of truth
- Data and control flow
- Failure, recovery, and consistency behavior
- Compatibility, migration, security, and operational boundaries

Record each source's status, scope, and rationale. Proposed or superseded documents are evidence of history, not governing decisions. When sources conflict, report the conflict rather than silently choosing the most convenient one.

If no explicit architecture exists, reconstruct the implicit decisions from repeated implementation patterns and tests. Label them inferred; absence of documentation is not proof of poor architecture.

## 3. Reconstruct the as-built architecture

Trace representative success and failure paths through the running shape of the system:

```text
entry point → orchestration → owning modules → state/external effects → outcome
```

Map the applicable elements:

- Modules, their interfaces, and responsibilities
- Call and dependency direction
- Sources of truth, identity, state transitions, and persistence
- Events, queues, concurrency, retries, cancellation, and consistency
- External systems, adapters, trust boundaries, and deployment units
- Tests, observability, rollout, recovery, and migration paths

Confirm runtime ownership through behavior, calls, and state mutation—not folder names or diagrams alone. Use targeted history to explain why consequential seams exist. Distinguish confirmed facts, inference, and unknowns.

This step is complete when the important outcomes and invariants can be traced to owners, dependencies, and state.

## 4. Evaluate the criteria

Apply each relevant criterion and mark non-applicable ones explicitly for a full audit:

- **Purpose fit:** The architecture supports the current product and operational outcomes without accidental constraints or unused generality.
- **Architecture alignment:** As-built responsibilities, interfaces, dependencies, and sources of truth agree with governing decisions—or diverge for an evidenced reason.
- **Ownership and locality:** Every material invariant and state transition has one clear owner; related change and diagnosis remain concentrated.
- **Interface depth:** Callers receive useful capability without learning implementation detail, coordinating hidden protocols, or duplicating policy.
- **Dependency integrity:** Dependency direction follows responsibility; cycles, reach-through, and cross-layer guesses do not distribute knowledge.
- **State and data integrity:** Identity, authority, persistence, consistency, retention, migration, and deletion form one coherent lifecycle.
- **Resilience:** Failure, timeout, retry, concurrency, cancellation, degradation, and recovery preserve defined invariants.
- **Security and privacy:** Trust boundaries, authorization, validation, secrets, sensitive data, and abuse controls live with the responsible owner.
- **Performance and scale:** Cost, latency, fan-out, contention, allocation, and growth are bounded for representative workloads.
- **Operability:** The system can be observed, diagnosed, contained, rolled out, rolled back, and recovered by a clear owner.
- **Testability:** Important behavior is provable through stable interfaces, including failure and migration paths.
- **Evolvability:** Expected changes can be made locally; temporary compatibility mechanisms and paths have explicit retirement conditions.

For each judgment, show:

```text
evidence → architectural property → present consequence or future pressure
```

Use qualitative ratings:

- **Strong:** Evidence shows the criterion creates leverage or prevents failure.
- **Adequate:** It fits current needs with bounded, understood tradeoffs.
- **Concern:** Evidence shows recurring friction or a credible risk under named conditions.
- **Critical:** The shape already causes serious harm or blocks required outcomes.
- **Unknown:** Evidence is insufficient; name the cheapest discriminating observation.

Avoid a numeric aggregate score: one critical source-of-truth flaw can matter more than many strong criteria.

## 5. Classify alignment and drift

For each applicable governing decision, classify:

- **Aligned:** The implementation preserves the decision and its rationale.
- **Intentional exception:** Divergence has an evidenced reason, bounded scope, owner, and review or removal condition where temporary.
- **Implementation drift:** The governing decision still serves the system, but implementation bypasses or contradicts it.
- **Architecture drift:** The as-built system has established a coherent newer reality and the governing decision is stale or no longer useful.
- **Unresolved:** Evidence cannot distinguish accidental drift from an intentional or obsolete decision.

Neither documentation nor code wins automatically. Recommend the correct reconciliation: change implementation, update the architecture decision, govern an exception, or gather evidence. Include the blast radius across other owners and features.

## 6. Find systemic causes

Cluster related observations around violated architectural properties. Do not produce a bag of local code smells.

Distinguish:

- A local implementation defect inside an adequate architecture
- A weak interface or module that should be deepened
- A misplaced or missing owner that requires architectural reshaping
- A deliberate tradeoff that remains acceptable until a named threshold
- Documentation or decision debt where the system is coherent but its governing model is stale

Treat duplicated truth, caller-enforced conventions, shotgun change, recurring cross-owner failures, untestable seams, and permanent compatibility paths as systemic signals. Confirm their reach before calling them architectural problems.

## 7. Recommend proportionate action

Group recommendations by response depth:

- **Preserve:** Architecture that is earning leverage, locality, or reliability
- **Clarify:** Update decisions, interfaces, ownership, or documentation without reshaping runtime behavior
- **Correct locally:** Repair an implementation that violates an adequate design
- **Deepen:** Strengthen an existing owner or interface so callers stop carrying its complexity
- **Reshape:** Move ownership, consolidate truth, reverse a dependency, or introduce/remove a justified seam
- **Investigate:** Resolve an unknown with a named test, trace, benchmark, history check, or operational observation

Prioritize by consequence, likelihood, propagation breadth, and correction cost. State what should trigger each change and what valuable property must survive it. Recommendations remain architectural direction, not task decomposition.

## Completion criteria

The assessment is complete when:

- The target's purpose and representative flows are clear
- Governing and as-built architecture are independently evidenced
- Every material criterion has a rating, consequence, and confidence level
- Alignment findings distinguish implementation drift from architecture drift
- Systemic conclusions trace across affected owners or paths
- Strengths worth preserving are as explicit as weaknesses
- Recommendations match the demonstrated depth of each problem
- Unknowns have a concrete proof path

## Final response

Lead with the architectural verdict, then present:

```text
Architecture map: <owners, interfaces, dependencies, state, and key flows>
Criteria: <strong, adequate, concern, critical, or unknown with evidence>
Alignment: <aligned, exceptions, implementation drift, architecture drift>
Systemic strengths: <properties to preserve>
Systemic risks: <ranked causal clusters and consequences>
Direction: <preserve, clarify, correct, deepen, reshape, investigate>
Confidence: <confirmed facts, inference, and unknowns>
```

Use file references and small diagrams only where they materially help the user verify or understand the architecture. Do not emit line-level review comments unless the user asks for code review.
