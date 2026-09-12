---
name: feature
description: Orchestrate a software feature across definition, solution architecture, planning, and implementation while preserving decisions, asking proposition-led questions at the right phase, routing work by complexity, and resuming from the first incomplete or stale gate. Use when the user wants end-to-end feature development or explicitly invokes the feature lifecycle. Requires the companion skills product-definition, solution-architecture, feature-planning, and feature-implementation for full-fidelity execution.
license: MIT
---

# Feature Lifecycle

Guide one feature through:

```text
Define → Architect → Plan → Implement
```

This is a thin coordinator, not a duplicate mega-prompt. Use the installed companion skills as the phase authorities, reading each companion only when its phase is active:

```text
Define      product-definition
Architect   solution-architecture
Plan        feature-planning
Implement   feature-implementation
```

If a required companion is unavailable, identify the missing skill and stop at that boundary. Do not imitate a missing phase from memory or install external content without authorization.

## 1. Establish terminal scope

Infer the requested stopping point from the user's words:

- “Explore,” “shape,” or “define” ends after Definition.
- “Design” or “architect” ends after Architecture.
- “Plan” ends after Planning.
- “Build,” “implement,” “complete,” or an explicit end-to-end request includes Implementation.

Ask only when the intended stopping point materially changes whether repository mutations are authorized. Never treat a request to understand or plan as authorization to edit code.

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

Inspect available conversation artifacts and repository evidence. Start at the first phase that is incomplete or whose inputs are stale. Do not rerun a completed phase merely because its document format differs.

A correction to an upstream decision supersedes the old entry. Mark only dependent downstream decisions, artifacts, tasks, or implementation slices stale; reopen those branches and preserve unaffected work.

## 4. Run phase authorities and gates

### Definition gate

Use `product-definition`. The gate requires confirmed persona, desired outcomes, use cases, acceptance criteria, first slice, non-goals, trust boundaries, success signals, and explicit deferrals.

### Architecture gate

Use `solution-architecture`. Research the repository before asking architectural questions. The gate requires owners, interfaces, invariants, sources of truth, flows, affected-path disposition, failure and migration behavior, proof checkpoints, and explicit deferrals.

### Planning gate

Use `feature-planning`. The gate requires coherent slices, dependency waves, single ownership of shared interfaces, complexity and model tiers, executable task packets, integration proofs, rollout/reversal gates, and acceptance coverage.

### Implementation gate

Use `feature-implementation` only when the terminal scope authorizes repository changes. The gate requires all in-scope outcomes demonstrated, cross-slice integration verified, repository checks satisfied in proportion to risk, and residual uncertainty reported precisely.

At each gate, reconcile the companion's output into the lifecycle ledger. Do not silently proceed past unresolved consequential decisions. Explicit deferral is allowed only when its consequence and forcing event are recorded. Once the gate is confirmed, continue to the next phase within the already authorized terminal scope; do not request the same authorization again. Gate approval does not broaden that scope.

## 5. Keep questions at the right layer

The lifecycle is questionnaire-led, not questionnaire-heavy:

- Definition asks about people, value, behavior, scope, trust, and success.
- Architecture determines repository facts itself, then asks only consequential ownership or tradeoff judgments.
- Planning determines dependencies itself, then asks only delivery, rollout, reversibility, verification, parallelism, and resource preferences.
- Implementation acts autonomously within the approved contracts and asks only when evidence changes product meaning, architecture, scope, risk, permissions, or external effects.

Every question must advance a decision frontier. Prefer a concrete recommendation with `Y / N / ?`, `A / B / C`, or a named `1–5` tradeoff; always accept richer prose. Never force the user's insight into the shortcut format.

## 6. Orchestrate models and delegation strategically

When routing is supported and authorized, the strongest permitted reasoning model owns lifecycle state, phase gates, decomposition, shared contracts, contradiction resolution, and final synthesis. Companion skills may route bounded work to capability tiers appropriate to remaining complexity.

Parallelize only independent work with stable boundaries. Do not assign multiple agents the same interface, source of truth, migration, or integration point. Lower-capability models receive explicit goals, technical decisions, scope, invariants, proof, deliverables, escalation conditions, and permissions. They escalate when evidence raises complexity instead of inventing architecture.

Do not silently change the user's selected model, increase cost, or assume delegation exists. Without routing, use the current permitted model, including for available subagents; without subagents, perform the roles locally.

## 7. Close the lifecycle

At the requested stopping point, report:

```text
Outcome       What is now defined, designed, planned, or delivered
Decisions     Consequential confirmed choices and explicit deferrals
Evidence      Research, repository paths, proofs, and verification
Artifacts     Definition, architecture, plan, and changed code as applicable
Residual      Stale branches, risks, missing permissions, or none known
Next gate     The next phase, or completion
```

Do not claim lifecycle completion when only documents exist for an implementation-authorized request. Do not deploy, publish, merge, commit, or mutate external systems unless the user requested or separately authorized that action.
