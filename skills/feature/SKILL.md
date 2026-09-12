---
name: feature
description: Orchestrate a feature through definition, solution architecture, planning, and implementation while preserving decisions and resuming stale work. Use for an explicitly end-to-end feature request or when the user invokes the full feature lifecycle; composes product-definition, solution-architecture, feature-planning, and feature-implementation.
license: MIT
---

# Feature Lifecycle

Guide one feature through:

```text
Define → Architect → Plan → Implement
```

The coordinator owns cross-phase state and sequencing; installed companions own the phase workflows. Read each companion only while its phase is active:

```text
Define      product-definition
Architect   solution-architecture
Plan        feature-planning
Implement   feature-implementation
```

If a required companion is unavailable, identify it and stop at that boundary. External installation requires user authorization.

## 1. Establish terminal scope

Infer the requested stopping point from the user's words:

- “Explore,” “shape,” or “define” ends after Definition.
- “Design” or “architect” ends after Architecture.
- “Plan” ends after Planning.
- “Build,” “implement,” “complete,” or an explicit end-to-end request includes Implementation.

Ask only when the intended stopping point materially changes whether repository mutations are authorized. Repository edits require an implementation-scoped request.

## 2. Create the feature ledger

Read [references/feature-ledger.md](references/feature-ledger.md). Keep one compact lifecycle ledger with:

```text
Decision status  confirmed | rejected | unresolved | inferred | superseded
Phase status     not-started | active | gated | stale | complete
Provenance       user | evidence | repository | delegated analysis
Dependency       upstream decisions and downstream artifacts affected
```

The ledger prevents repeated questions and silent reinterpretation. Accept compact answers, prose, partial replies, corrections, and unsolicited constraints at every interactive phase. Preserve conditions attached to answers.

## 3. Resume instead of restarting

Inspect available conversation artifacts and repository evidence. Start at the first phase that is incomplete or whose inputs are stale. Preserve a completed phase when its decisions remain valid, regardless of document format.

A correction to an upstream decision supersedes the old entry. Mark only dependent downstream decisions, artifacts, tasks, or implementation slices stale; reopen those branches and preserve unaffected work.

## 4. Run one phase authority at a time

| Phase | Authority | Gate |
| --- | --- | --- |
| Define | `product-definition` | Its Product Definition completion criteria pass |
| Architect | `solution-architecture` | Its architecture decision completion criteria pass |
| Plan | `feature-planning` | Its executable plan completion criteria pass |
| Implement | `feature-implementation` | Its delivery completion criteria pass |

Load only the active companion and the references that companion selects. The phase authority owns its research, question strategy, complexity routing, delegation, artifact, and completion criteria; the umbrella owns ordering, lifecycle scope, and cross-phase state.

At each gate, reconcile the companion's output into the lifecycle ledger. Resolve consequential decisions or defer them with a consequence and forcing event. A confirmed gate advances within the already authorized terminal scope without repeating the authorization question; it never broadens that scope. Run Implementation only when the terminal scope authorizes repository changes.

Definition, Architecture, and Planning remain proposition-led decision sessions. Accept compact choices, prose, qualifiers, corrections, and unsolicited constraints. Implementation acts within the approved contracts and reopens an upstream phase when evidence changes product meaning, architecture, scope, risk, permissions, or external effects.

When routing or delegation is supported and authorized, let each phase authority apply its own complexity rules. The lifecycle coordinator retains the ledger, phase gates, shared decisions, and contradiction resolution. Otherwise use the current permitted model and perform unavailable roles locally.

## 5. Close the lifecycle

At the requested stopping point, report:

```text
Outcome       What is now defined, designed, planned, or delivered
Decisions     Consequential confirmed choices and explicit deferrals
Evidence      Research, repository paths, proofs, and verification
Artifacts     Definition, architecture, plan, and changed code as applicable
Residual      Stale branches, risks, missing permissions, or none known
Next gate     The next phase, or completion
```

For an implementation-scoped request, lifecycle completion requires delivered behavior rather than documents alone. Deployment, publication, merging, commits, and external mutations require explicit request or separate authorization.
