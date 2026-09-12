# Architecture Assessment Criteria

Use the criteria that bear on the assessment question. Account for every criterion in a broad audit and mark non-applicable ones.

- **Purpose fit:** The architecture supports current product and operational outcomes without accidental constraints or unused generality.
- **Architecture alignment:** As-built responsibilities, interfaces, dependencies, and sources of truth agree with governing decisions or diverge for an evidenced reason.
- **Ownership and locality:** Every material invariant and state transition has one clear owner; related change and diagnosis remain concentrated.
- **Interface depth:** Callers receive useful capability without learning implementation detail, coordinating hidden protocols, or duplicating policy.
- **Dependency integrity:** Dependency direction follows responsibility; cycles, reach-through, and cross-layer guesses do not distribute knowledge.
- **State and data integrity:** Identity, authority, persistence, consistency, retention, migration, and deletion form one coherent lifecycle.
- **Resilience:** Failure, timeout, retry, concurrency, cancellation, degradation, and recovery preserve defined invariants.
- **Security and privacy:** Trust boundaries, authorization, validation, secrets, sensitive data, and abuse controls live with the responsible owner.
- **Performance and scale:** Cost, latency, fan-out, contention, allocation, and growth are bounded for representative workloads.
- **Operability:** The system can be observed, diagnosed, contained, rolled out, rolled back, and recovered by a clear owner.
- **Testability:** Important behavior is provable through stable interfaces, including failure and migration paths.
- **Evolvability:** Expected changes remain local; temporary compatibility mechanisms have explicit retirement conditions.

For each judgment, show:

```text
evidence → architectural property → present consequence or future pressure
```

Use qualitative ratings:

- **Strong:** The criterion creates leverage or prevents failure.
- **Adequate:** It fits current needs with bounded, understood tradeoffs.
- **Concern:** It creates recurring friction or a credible risk under named conditions.
- **Critical:** The shape already causes serious harm or blocks required outcomes.
- **Unknown:** Evidence is insufficient; name the cheapest discriminating observation.

One critical source-of-truth flaw can outweigh many strong criteria, so preserve the individual judgments instead of calculating an aggregate score.
