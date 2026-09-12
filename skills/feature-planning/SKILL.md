---
name: feature-planning
description: Turn an approved product definition and solution architecture into an executable delivery plan through a short, proposition-led planning session, dependency-aware slices, explicit task packets, complexity classification, model routing, and verification gates. Use after feature definition and architecture, before implementation. Do not use for product discovery, architecture design, code changes, or post-build assessment.
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

Inspect the repository only enough to verify current paths, build/test entry points, dependency boundaries, and whether architecture assumptions remain true. Do not ask the user to repeat available information.

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

Work in short proposition-led rounds. Give evidence, a recommendation, and the consequence, then accept `Y / N / ?`, `A / B / C`, `1–5`, free text, or any mixture. Preserve qualifiers, corrections, and unsolicited constraints. Do not ask questions whose answers can be inferred safely from the approved contracts or repository.

Maintain a planning decision ledger:

```text
confirmed | rejected | unresolved | inferred | superseded
```

If a correction changes product meaning or architecture ownership, mark affected planning branches stale and return it to that phase. Do not locally patch an upstream contradiction.

## 3. Plan coherent slices

Define vertical or otherwise independently provable slices. Each slice must close an observable behavior or a named technical proof; avoid layers of disconnected scaffolding.

For each slice, specify:

- Outcome and acceptance criteria covered
- Owning module and interfaces changed
- Invariants and behavior that must remain unchanged
- Prerequisites and downstream consumers
- Migration, rollout, rollback, or cleanup gates
- Focused proof and integration proof

Order slices by dependency and learning value. Put design-disproving proofs early. For contract or data changes, explicitly plan sequences such as expand → migrate → switch → contract and name the deletion condition for temporary paths.

## 4. Classify complexity and route capability

Classify every task using ambiguity, coupling, blast radius, reversibility, novelty, and verification clarity:

```text
Mechanical              One explicit transformation; deterministic proof; low correction cost
Bounded                 Stable interface and local change; focused verification
Integrative             Multiple modules or behaviors must agree; sequencing requires judgment
Architectural/high-risk Ownership, public contract, security, concurrency, migration, or hard reversal
```

When model routing is supported and authorized, the strongest permitted reasoning model owns decomposition, shared contracts, dependency ordering, risk decisions, and final synthesis. Route reduced work to the least costly model that can reliably perform it:

```text
Mechanical              → fast capable model
Bounded                 → capable coding model
Integrative             → strong coding/reasoning model with coordinator oversight
Architectural/high-risk → strongest permitted reasoning model; retain or closely supervise
```

Do not silently override the user's model or cost constraints. Without routing, retain complexity classes but assign work to the current permitted model. Upgrade or retain a task when its remaining ambiguity or risk exceeds the assigned tier.

## 5. Design safe delegation

Use parallel work only for independent tasks with stable interfaces and disjoint ownership. Shared schemas, public contracts, migrations, generated artifacts, and integration points have one coordinator. Arrange work into dependency waves, with an integration gate between waves.

For substantial plans, delegation may independently analyze the dependency graph, verification strategy, and migration/rollout risks. The coordinator must reconcile these views against evidence; consensus is not proof. For narrow plans or environments without delegation, perform the roles locally.

Write every executable unit as a task packet:

```text
Goal             One observable outcome
Context          Approved decisions and relevant repository facts
Technical plan   Owner, interfaces, symbols, sequence, and decided approach
Scope            Allowed modules/files and explicit exclusions
Invariants       Behavior and contracts that must remain true
Proof            Focused and integration checks
Deliverable      Expected code, tests, evidence, and report
Escalation       Evidence that invalidates assumptions or raises complexity
Permissions      Allowed mutations and forbidden external actions
```

Give lower-capability models decisions to execute, not architecture to invent.

## 6. Produce the feature plan

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
