# Product Definition artifact

Synthesize the approved decisions into a concise product source of truth. Adapt the form to the idea; omit empty sections rather than filling them with speculation.

```markdown
# Product Definition: <working name>

## Product thesis
<Who makes what progress, in which moment, and why this product is meaningfully better.>

## Problem and current alternative
<The observed problem, its consequence, and how users handle it today.>

## Target users
### Primary
<Actor, context, capability, and motivation>

### Secondary or excluded
<Who matters later or is intentionally outside version one>

## Product principles
- <Decision rule that resolves future tradeoffs>

## Core use cases
### UC-01 — <outcome>
**Trigger:** <starting event>
**Journey:** <essential interaction>
**Success:** <observable end state>
**Failure/recovery:** <expected behavior>

## Acceptance criteria
- AC-01 [user]: Given <context>, when <action>, then <observable outcome>.

## Version one
### Must
- R-01 [user]: <observable capability>

### Should
- R-02 [user]: <valuable but negotiable capability>

### Later
- R-03 [inferred]: <deliberately deferred possibility>

## Non-goals
- <tempting but excluded scope and why>

## Trust and control
<Permissions, privacy, confirmation, reversibility, explanation, and abuse boundaries.>

## Experience contract
<Required states, feedback, accessibility, interruption, and error behavior without prescribing technical implementation.>

## Success and counter-metrics
- Success: <behavior or outcome>
- Counter-metric: <harm or false optimization to prevent>
- Invalidation signal: <evidence that would challenge the premise>

## Assumptions and evidence
- A-01 [inferred, reversible]: <assumption and cheapest test>
- E-01 [evidence]: <finding and source>

## Open decisions
- Q-01: <explicitly deferred decision, owner, trigger, and consequence>
```

## Synthesis rules

- Write one coherent product, not a transcript of the interview.
- Convert confirmed answers into decisions; retain the user's wording where it carries meaning.
- Keep implementation choices out unless they are genuine product constraints.
- State tensions honestly instead of smoothing contradictory preferences together.
- Make version one narrow enough to test the thesis and complete enough to deliver the core outcome.
- Give every metric a counter-metric or guardrail when optimizing it could degrade user value.
- Keep deferred decisions visible with the event that will force resolution.

## Final review

Before presenting the draft, verify:

- Each Must requirement supports a core use case.
- Each core use case has observable acceptance criteria.
- Each use case supports the product thesis.
- Non-goals prevent at least the most likely scope drift.
- Trust, failure, and recovery behavior match the product's actual power.
- Success signals can distinguish value from activity.
- No inferred statement is presented as a user decision.
