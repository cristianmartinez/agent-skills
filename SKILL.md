---
name: product-definition
description: Explore and shape an early product or feature idea through an interactive, proposition-led interview, then synthesize the decisions into a rigorous Product Definition. Use when the user wants to discover blind spots, define what to build, challenge an idea, or turn “I need to build…” into a product brief before architecture or implementation.
---

# Product Definition

Turn an initial product idea into a decision-complete Product Definition. The conversation is the primary work: reveal consequential possibilities the user has not considered, make tradeoffs easy to answer, and preserve the user's judgment.

Do not design the technical architecture or begin implementation during this skill unless the user explicitly expands the request after approving the Product Definition.

## Opening

Restate the idea in one or two sentences, including the outcome you currently infer. Label it provisional. Then begin the first discovery round; do not front-load a questionnaire or ask the user to explain everything.

## Build a discovery tree

Map decisions as a tree. A decision enters the **frontier** when its prerequisites are settled enough to answer without pretending certainty.

Explore the applicable branches:

- Actor, context, triggering moment, and desired progress
- Existing alternative and why it fails
- Value proposition and product principles
- Core workflow, frequency, and time-to-value
- Scope, non-goals, and version-one boundary
- Trust, privacy, permissions, safety, and abuse
- Failure, recovery, reversibility, and user control
- Collaboration, ownership, and lifecycle
- Accessibility, localization, and constrained environments
- Adoption, distribution, pricing, or incentives
- Success signals, counter-metrics, and invalidation conditions
- Strategic leverage, adjacent users, and future pressure

Use [references/discovery-lenses.md](references/discovery-lenses.md) when the idea is broad, unfamiliar, high-consequence, or the frontier appears empty suspiciously early.

## Work in rounds

Ask four to seven frontier questions per round. Prefer concrete assertions the user can accept or reject. Include:

- Core decisions needed to advance the definition
- At least one applicable blind-spot probe that could materially change the product
- A recommendation and short reason for each answer
- The consequence of the decision when it is not obvious

Use the lowest-friction response type that preserves the decision:

```text
Y / N / ?       Accept, reject, or explore an assertion
1–5             Choose a position on a named tradeoff
A / B / C       Select genuinely categorical alternatives
free text       Only when the user's language or novel input is the product
```

Format each question as:

```markdown
**Q1 — <decision title>**
<Concrete proposition or tradeoff and its consequence.>

Recommended: **Y** — <brief product reasoning>
Answer: `Y / N / ?`
```

For a scale:

```markdown
**Q2 — Automation vs control**
How much should the product act without confirmation?

`1` = always ask · `5` = act autonomously when reversible
Recommended: **3** — <brief product reasoning>
Answer: `1–5`
```

Tell the user they can answer compactly, for example `1Y 2=4 3N 4?`. Accept prose and partial answers naturally.

## Make discovery useful

Do not ask questions merely because a category exists. Every question must change the definition, expose a risk, distinguish alternatives, or reveal a new opportunity.

Find facts yourself using available repository, research, or product context. Ask the user for judgments, preferences, constraints only they know, and corrections to your interpretation.

Do not hide the interesting option inside a generic question. Propose it explicitly:

- Weak: “What edge cases matter?”
- Strong: “Should a failed automated action leave a reviewable draft instead of rolling back invisibly?”

Probe second-order effects. Ask what changes when usage becomes frequent, collaborative, adversarial, regulated, slow, interrupted, or successful at much larger scale—but only where plausible.

Maintain a private decision ledger after every answer:

```text
confirmed | rejected | unresolved | inferred
```

Track contradictions and dependencies. Recompute the frontier after each round instead of following a fixed script.

## Use uncertainty well

Ask for clarification when:

```text
uncertainty × consequence of error × correction cost × propagation breadth
```

is material. Proceed with an explicit reversible assumption when that value is low.

When the user answers `?`, explain the real alternatives and recommend a choice. Research factual uncertainty yourself. If evidence changes an earlier recommendation, say so directly.

## Synthesize with the strongest available reasoning

Once no material frontier remains, use the strongest reasoning capability available in the current environment for synthesis. A skill cannot silently change the user's selected model; when model routing is supported and authorized, reserve the strongest model for this synthesis rather than routine question formatting.

Read [references/product-definition.md](references/product-definition.md) and draft the Product Definition from the decision ledger. Preserve provenance: distinguish what the user decided, what evidence supports, and what remains inferred.

Present the draft for correction. The session completes only when:

- The user confirms the definition reflects their intent
- Every material decision is resolved or explicitly deferred with consequence
- Version one, non-goals, and success signals are clear
- No important requirement depends on a silent assumption

After confirmation, offer architecture mapping or execution planning as a separate next step. Do not let implementation details retroactively masquerade as product requirements.
