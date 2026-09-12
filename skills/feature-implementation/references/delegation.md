# Complexity Routing and Delegation

Load this reference for substantial features or whenever model routing, subagents, or parallel work is in play.

## Complexity classes

- **Mechanical:** One explicit transformation or lookup, one owner, deterministic proof, and low correction cost.
- **Bounded:** Stable interface and outcome; local or isolated implementation with focused tests.
- **Integrative:** Several modules or behaviors must agree; sequencing or interaction effects require judgment.
- **Architectural/high-risk:** Ownership, public interfaces, or sources of truth need judgment; or security, concurrency, migration, destructive, or hard-to-reverse effects retain material risk.

Classify remaining work, then reduce complexity before routing it. When routing is supported and authorized, use the strongest permitted reasoning model for orchestration, shared contracts, and synthesis:

```text
Mechanical              → fast capable model
Bounded                 → capable coding model
Integrative             → strong coding/reasoning model with coordinator oversight
Architectural/high-risk → strongest permitted reasoning model; retain or closely supervise
```

Use the least costly model that can reliably complete the reduced task. Without routing, keep the classification and use the current permitted model. Raise the tier or return work to the coordinator when evidence raises its class.

## Roles and ownership

Parallelize only independent work whose coordination cost is justified:

- **Explorer:** Trace a subsystem, inventory callers or tests, or validate an assumption without editing.
- **Slice implementer:** Own one coherent slice behind a stable interface with disjoint code ownership and focused proof.
- **Verifier:** Exercise acceptance behavior, failure paths, or integration independently of implementer conclusions.

The coordinator owns the implementation contract, shared interfaces, source-of-truth decisions, migration sequence, ledger, integration, and final verification. Stabilize shared schemas and contracts before dependent work. Give concurrent agents disjoint ownership; use isolated worktrees when available and serialize shared files otherwise.

## Task packet

```text
Goal             One observable outcome
Context          Why the work exists and relevant repository facts
Technical plan   Decided approach, owner, interfaces, symbols, and sequence
Scope            Allowed files/modules and explicit exclusions
Invariants       Behavior and contracts that must remain true
Proof            Commands or observable acceptance checks
Deliverable      Expected code, tests, evidence, and concise report
Escalation       Conditions that invalidate assumptions or raise complexity
Permissions      Allowed mutations and forbidden external actions
```

Give a delegate decisions to execute and local choices that cannot change product meaning or shared design. Contradictions, missing interfaces, failed invariants, insufficient scope, disproven plans, and higher complexity return to the coordinator with evidence.

Work in dependency waves. Inspect returned diffs and evidence, integrate them, and restore a green baseline before dependent waves. Agent summaries and consensus are not proof; rerun decisive integration signals. Respect the user's selected model, cost, permissions, and available concurrency.
