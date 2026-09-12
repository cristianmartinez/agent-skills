---
name: feature-planning
description: Turn an approved feature definition and solution architecture into an executable, dependency-aware delivery plan. Use after product and architecture decisions are settled to plan slices, task packets, model routing, rollout, and verification; produces planning rather than code changes or post-build assessment.
license: MIT
---

# Feature Planning

Convert approved product and architecture decisions into a plan an implementation coordinator can execute without rediscovering the feature. Preserve the decisions; expose sequencing, ownership, proof, rollout, and risk.

This skill plans but does not edit code. If either upstream contract is materially incomplete, return to the appropriate phase instead of hiding ambiguity inside tasks.

## 1. Establish planning inputs

Extract:

```text
Definition    Persona, outcomes, use cases, acceptance criteria, scope, non-goals
Architecture  Owners, interfaces, invariants, flows, migrations, proof checkpoints
Constraints   Repository rules, compatibility, security, performance, delivery limits
Unknowns      Deferred decisions and technical proofs, each with consequence
```

Inspect the repository only enough to verify current paths, build/test entry points, dependency boundaries, and whether architecture assumptions remain true. Derive available facts directly and reserve user questions for missing judgments.

## 2. Resolve the planning frontier

Derive factual sequencing from repository and architecture evidence. Ask only consequential planning judgments, such as:

- Which product-complete slice should deliver value first
- Rollout, compatibility, migration, rollback, and removal posture
- Reversibility versus speed
- Milestone and review boundaries
- Acceptable parallelism and coordination cost
- Verification depth and release gates
- Model, cost, latency, or execution-environment constraints
- Stop conditions when proofs contradict the design

Work in short proposition-led rounds. Give evidence, a recommendation, and the consequence, then accept `Y / N / ?`, `A / B / C`, `1–5`, free text, or any mixture. Preserve qualifiers, corrections, and unsolicited constraints. Ask only for decisions that cannot be inferred safely from approved contracts or repository evidence.

Maintain a planning decision ledger:

```text
confirmed | rejected | unresolved | inferred | superseded
```

If a correction changes product meaning or architecture ownership, mark affected planning branches stale and return the contradiction to its owning phase.

## 3. Plan coherent slices

Define vertical or otherwise independently provable slices. Each slice must close an observable behavior or a named technical proof, producing integrated behavior instead of disconnected scaffolding.

For each slice, specify:

- Outcome and acceptance criteria covered
- Owning module and interfaces changed
- Invariants and behavior that must remain unchanged
- Prerequisites and downstream consumers
- Migration, rollout, rollback, or cleanup gates
- Focused proof and integration proof

Order slices by dependency and learning value. Put design-disproving proofs early. For contract or data changes, explicitly plan sequences such as expand → migrate → switch → contract and name the deletion condition for temporary paths.

## 4. Design executable work

Classify each task as **mechanical**, **bounded**, **integrative**, or **architectural/high-risk** using ambiguity, coupling, blast radius, reversibility, novelty, and verification clarity. Every executable unit needs an explicit task packet, even when one agent owns the whole plan.

For a substantial plan, a multi-agent request, or an environment where model routing or parallel execution is being considered, read [references/execution-design.md](references/execution-design.md). Keep shared interfaces, migrations, and integration under one coordinator.

## 5. Produce the feature plan

Read [references/feature-plan.md](references/feature-plan.md) and adapt it to the feature. Use the strongest permitted reasoning capability for synthesis.

The plan is ready when:

- Every in-scope outcome and acceptance criterion is covered exactly where it becomes provable
- Dependency waves are valid and concurrent tasks have disjoint ownership
- Shared interfaces, migrations, and integration remain coordinator-owned
- Every task has a complexity class, capability tier, explicit packet, and proof
- Rollout, rollback, compatibility, cleanup, and stop conditions are explicit where relevant
- The implementation coordinator can begin without rediscovering product meaning or architecture
- Unresolved items are explicit, with owner, consequence, and gate

Present the draft for correction. The phase completes only when the user confirms consequential planning decisions or explicitly defers them. End with an implementation handoff, not code changes.
