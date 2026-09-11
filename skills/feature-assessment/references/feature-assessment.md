# Feature Assessment Template

Use this structure for a durable assessment of a substantial implemented feature. Adapt it to the evidence; omit sections that do not apply.

```markdown
# <Feature> — As-Built Assessment

## Verdict

<What the feature is, whether its current shape is sound, and the most important reason.>

## Scope and Evidence

- **Feature surface:**
- **Assessment question:**
- **Included paths:**
- **Excluded paths:**

| Evidence | What it confirms | Confidence |
| --- | --- | --- |
| `<path, test, trace, history, or document>` | <fact> | <confirmed/inferred/unknown> |

## Intended and Observed Behavior

| Scenario | Stated intent | Observed behavior | Gap |
| --- | --- | --- | --- |
| <scenario> | <documented outcome> | <as-built outcome> | <none or mismatch> |

## How It Works

### User model

<Trigger, workflow, states, outcomes, errors, recovery, and controls.>

### System model

<Entry point → owners/interfaces → state and effects → outcome.>

### State and ownership

| Concept or transition | Owner | Source of truth | Invariant or contract |
| --- | --- | --- | --- |
| <concept> | <module/system> | <authority> | <rule> |

## What Is Good

| Strength | Evidence | Consequence worth preserving |
| --- | --- | --- |
| <property> | <evidence> | <user/engineering value> |

## What Is Weak

| Priority | Class | Finding and evidence | Current or future consequence | Trigger/likelihood |
| --- | --- | --- | --- | --- |
| <high/medium/low> | <defect/limitation/tradeoff/architecture/operations/debt/unknown> | <finding> | <impact> | <conditions> |

## Recommendations

### Keep

- <behavior or design to preserve>

### Improve now

- <proportionate response and expected value>

### Revisit at threshold

- <tradeoff and measurable trigger>

### Investigate

- <unknown and cheapest discriminating observation>

## Confidence and Open Questions

- **Confirmed:**
- **Inferred:**
- **Unknown:**
```
