# Feature Assessment Lenses

Apply only lenses that can materially affect the feature:

- **Product coherence:** The workflow solves a recognizable problem consistently; states, controls, and failure behavior are understandable.
- **Domain integrity:** Concepts and invariants are explicit rather than repeatedly reconstructed from primitives and conventions.
- **Architecture:** Responsibility is local to a clear owner; interfaces contain complexity and sources of truth remain singular.
- **Correctness and resilience:** Assumptions, edge cases, concurrency, retry, cancellation, and recovery preserve outcomes.
- **Data lifecycle:** Identity, persistence, compatibility, migration, retention, and deletion are coherent.
- **Security and privacy:** Trust boundaries, authorization, validation, sensitive data, and abuse controls live at the right owner.
- **Performance and scale:** Cost, latency, fan-out, contention, allocation, and growth are bounded under representative use.
- **Operability:** Maintainers can observe, diagnose, contain, roll back, and recover the feature.
- **Testability and changeability:** Tests exercise meaningful interfaces and failure paths; expected changes remain local.

Connect each strength or weakness through:

```text
evidence → property of design or behavior → user or engineering consequence
```

Judge the feature's actual tradeoffs rather than aesthetics or generic checklists. State what a tradeoff buys, what it costs, and the condition that makes its cost unacceptable.

## Weakness classes

- **Defect:** Current behavior violates an evidenced contract or invariant.
- **Product limitation:** The feature intentionally or effectively excludes a meaningful use case.
- **Design tradeoff:** A cost accepted to gain another property; assess whether the original conditions still hold.
- **Architectural risk:** Ownership, interface, state, or dependency shape makes failure or future change systemic.
- **Operational risk:** Deployment, observability, recovery, or an external dependency threatens reliable operation.
- **Maintainability debt:** The feature works, but its implementation raises the cost or error rate of future change.
- **Unknown:** Evidence is insufficient; name the cheapest observation that would resolve it.
