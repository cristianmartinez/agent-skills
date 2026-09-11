---
name: feature-assessment
description: Reverse-engineer an implemented software feature and assess how it works, what is strong, what is flawed, and what should improve. Use when the user wants to understand an existing feature's behavior, architecture, history, risks, limitations, or quality without reviewing a particular diff. This is an as-built feature assessment, not code review or implementation.
license: MIT
---

# Feature Assessment

Explain and evaluate an implemented feature as a complete system. Reconstruct what users experience, how the implementation produces it, why it has its current shape, and where that shape succeeds or fails.

Stay read-only. Recommend improvements, but do not edit the feature unless the user separately asks for implementation.

## 1. Frame the assessment

Resolve these facts from the request and repository:

```text
Feature    The capability or workflow being assessed
Surface    Where users or other systems encounter it
Question   What the user most wants to understand or evaluate
Scope      Relevant product, platform, environment, or version limits
Evidence   Docs, examples, incidents, metrics, or concerns already supplied
```

Do not require a formal specification or fixed git comparison. If the target could refer to several features or paths, ask one compact scoping question. Otherwise state the interpreted scope and proceed.

Scale the work to the feature. A single validation rule may need a short note; a cross-system workflow may need a durable assessment using [references/feature-assessment.md](references/feature-assessment.md).

## Scale and delegate the assessment

Use one agent for a narrow feature with a short, well-localized path. For a substantial or cross-system feature, use independent parallel passes when the environment supports delegation and the added coverage justifies its cost:

- **Feature cartographer:** Reconstruct the user flow, system flow, state, ownership, and relevant history without judging quality.
- **Product and lifecycle assessor:** Evaluate product coherence, failure and recovery behavior, data lifecycle, user control, and meaningful limitations.
- **Engineering assessor:** Evaluate architecture, correctness, resilience, security, performance, operability, testability, and changeability.

Give independent passes the same target, scope, and raw evidence locations, but not prior conclusions or expected findings. Keep every pass read-only. Require confirmed facts, inferences, and unknowns from all passes, and evidence → property → consequence judgments from assessors. Split by lens rather than sending duplicate broad prompts.

Use available worker slots; the coordinator may own a pass and complete remaining work sequentially when delegation is limited or unavailable.

When delegating and model routing is available and compatible with the user's constraints, use fast capable models for bounded discovery and path tracing, strong reasoning models for judgment-heavy lenses, and the strongest available reasoning model for final synthesis. A skill cannot silently override a user-selected model or authorize additional cost; use the best available capability when routing is unavailable.

The coordinating agent must inspect decisive evidence and synthesize after all passes finish. Reconcile contradictions, deduplicate shared observations, and preserve distinct consequences. Do not vote or treat agreement as proof; keep material unresolved conflicts explicit.

## 2. Discover the feature footprint

Start from observable entry points and trace inward. Search for user-facing labels, routes, commands, events, configuration, public interfaces, persisted data, tests, and documentation associated with the feature.

Build an evidence-backed footprint across applicable layers:

- User or caller entry points
- Presentation and interaction state
- Orchestration and domain rules
- Sources of truth, identity, and persistence
- Background work and external integrations
- Authorization, configuration, flags, and rollout controls
- Failure handling, recovery, and observability
- Tests and documentation

Use targeted history, blame, issues, or design records when they explain why the feature took its current shape. Current behavior remains authoritative for the as-built assessment; historical intent explains but does not override it.

Follow at least one representative success path end to end. Follow important failure, recovery, cancellation, or migration paths when they materially affect the feature.

## 3. Reconstruct the as-built feature

Separate three views:

- **Stated intent:** What current specifications, documentation, or product language claim
- **Observed behavior:** What the system demonstrably does
- **Inferred design:** The responsibilities and rationale implied by code, tests, and history

Label each material statement as confirmed, inferred, or unknown. Do not invent an original product requirement from implementation details.

Explain the feature in two connected models:

1. **User model:** trigger, workflow, states, outcomes, errors, recovery, and controls.
2. **System model:** entry point → owning modules and interfaces → state transitions and external effects → returned or rendered outcome.

Name the source of truth, identity model, major invariants, and ownership seams. Use a compact flow or table when it makes three or more relationships easier to understand.

This step is complete when the user-facing behavior can be traced to the modules and state that produce it, with gaps explicitly named.

## 4. Assess from multiple lenses

Apply only lenses that can materially affect this feature:

- **Product coherence:** Does the workflow solve a recognizable problem consistently? Are states, controls, and failure behavior understandable?
- **Domain integrity:** Are concepts and invariants explicit, or reconstructed repeatedly from primitives and conventions?
- **Architecture:** Is responsibility local to a clear owner? Are interfaces deep enough, or does knowledge leak across callers? Are sources of truth duplicated?
- **Correctness and resilience:** What assumptions, edge cases, concurrency, retry, cancellation, and recovery behavior can break outcomes?
- **Data lifecycle:** Are identity, persistence, compatibility, migration, retention, and deletion coherent?
- **Security and privacy:** Are trust boundaries, authorization, validation, sensitive data, and abuse cases handled at the right owner?
- **Performance and scale:** Where do cost, latency, fan-out, contention, allocation, or unbounded growth emerge under representative use?
- **Operability:** Can maintainers observe, diagnose, contain, roll back, and recover the feature?
- **Testability and changeability:** Do tests exercise meaningful interfaces and failure paths? Can the feature evolve locally, or does change cause scattered edits?

For every strength or weakness, connect evidence to consequence:

```text
Evidence → property of the design or behavior → user or engineering consequence
```

Avoid aesthetic judgments and generic best-practice checklists. A tradeoff is not automatically a flaw; state what it buys, what it costs, and when that cost becomes unacceptable.

## 5. Classify weaknesses accurately

Use the narrowest fitting class:

- **Defect:** Current behavior violates an evidenced contract or invariant.
- **Product limitation:** The feature intentionally or effectively excludes a meaningful use case.
- **Design tradeoff:** A cost accepted to gain another property; assess whether the original conditions still hold.
- **Architectural risk:** Ownership, interface, state, or dependency shape makes failure or future change systemic.
- **Operational risk:** Deployment, observability, recovery, or external dependency behavior threatens reliable operation.
- **Maintainability debt:** The feature works, but its implementation increases the cost or error rate of future change.
- **Unknown:** Evidence is insufficient; name the cheapest observation that would resolve it.

Rank issues by consequence and likelihood, not code size or stylistic preference. Distinguish current harm from future pressure. Do not call a local imperfection architectural without evidence that its effects cross owners or recur across paths.

## 6. Form the verdict

Synthesize rather than dump observations. Answer:

- What the feature fundamentally is and how it works
- What was designed well and why it deserves to be preserved
- What is weak, under what conditions, and who experiences the consequence
- Whether the feature is locally improvable or needs architectural reshaping
- Which improvements have the greatest value relative to disruption
- Which unknowns prevent a confident judgment

Group recommendations by decision:

- **Keep:** Valuable behavior or design that future changes should preserve
- **Improve now:** Evidenced issue with a proportionate, actionable response
- **Revisit at threshold:** Acceptable tradeoff until a named scale, use case, or failure condition occurs
- **Investigate:** Missing evidence and the cheapest discriminating check

Do not turn recommendations into a file-by-file implementation plan. If a defect is found, describe it and its impact; use a separate debugging/fixing phase to establish and implement the repair.

## Completion criteria

The assessment is complete when:

- The feature's scope and representative behavior are clear
- The user and system models agree or their mismatch is explained
- Material claims distinguish confirmed facts, inference, and unknowns
- Strengths and weaknesses cite concrete evidence and consequences
- Applicable lifecycle and cross-cutting concerns are addressed
- Recommendations preserve what works and are proportional to demonstrated problems
- Remaining uncertainty has a named proof path

## Final response

For a conversational assessment, lead with the verdict, then show:

```text
How it works: <user and system flow>
What is good: <strengths worth preserving>
What is weak: <ranked flaws, tradeoffs, and risks>
Recommendation: <keep, improve, revisit, investigate>
Confidence: <confirmed facts, inferences, and unknowns>
```

Reference files and lines only where they help the user follow the feature or verify an important judgment. Do not emit line-level review comments unless the user asks for code review.
