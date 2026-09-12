---
name: feature-assessment
description: Reverse-engineer and assess an implemented feature as a complete user and system flow. Use to understand how an existing feature works, why it has its shape, what is strong or flawed, and what should improve; produces an as-built assessment rather than diff review or implementation.
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

A formal specification or fixed git comparison is optional. If the target could refer to several features or paths, ask one compact scoping question. Otherwise state the interpreted scope and proceed.

Scale the work to the feature. A single validation rule may need a short note; a cross-system workflow may need a durable assessment using [references/feature-assessment.md](references/feature-assessment.md).

Scale the assessment to the feature. Handle a short, localized path locally. For a substantial, cross-system, multi-agent, or model-routed assessment, read [references/parallel-assessment.md](references/parallel-assessment.md) before dispatching work.

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

Read [references/assessment-lenses.md](references/assessment-lenses.md) and apply only lenses that can materially affect this feature. Connect every judgment through evidence → property → user or engineering consequence.

## 5. Classify weaknesses accurately

Use the narrowest class defined in [references/assessment-lenses.md](references/assessment-lenses.md). Rank issues by consequence and likelihood, distinguish current harm from future pressure, and require cross-owner or recurring-path evidence before classifying a local imperfection as architectural.

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
