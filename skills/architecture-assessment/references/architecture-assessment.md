# Architecture Assessment Template

Use this structure for a durable assessment of a substantial feature, subsystem, or system. Adapt it to the target; omit non-applicable detail in a narrow assessment.

```markdown
# <Target> — Architecture Assessment

## Verdict

<Whether the architecture serves its current purpose, its strongest property, and its most important risk.>

## Scope and Purpose

- **Target:**
- **Responsibilities and outcomes:**
- **Current pressures:**
- **Included:**
- **Excluded:**

## Evidence

| Source | Status | Confirmed claim | Confidence |
| --- | --- | --- | --- |
| `<document, ADR, code path, test, trace, history, or metric>` | <governing/proposed/superseded/as-built> | <fact> | <confirmed/inferred/unknown> |

## Architecture Map

### Representative flows

<Entry point → orchestration → owners → state/effects → outcome.>

### Ownership and interfaces

| Responsibility or invariant | Owner | Interface and guarantee | Callers |
| --- | --- | --- | --- |
| <responsibility> | <module/system> | <contract> | <dependents> |

### State and dependencies

| State or dependency | Authority/direction | Lifecycle or constraint | Evidence |
| --- | --- | --- | --- |
| <state/system> | <source of truth or dependency direction> | <create/update/recover/migrate/delete> | <source> |

## Criteria Scorecard

| Criterion | Rating | Evidence → property → consequence | Confidence |
| --- | --- | --- | --- |
| Purpose fit | <strong/adequate/concern/critical/unknown/N/A> | <chain> | <level> |
| Architecture alignment | | | |
| Ownership and locality | | | |
| Interface depth | | | |
| Dependency integrity | | | |
| State and data integrity | | | |
| Resilience | | | |
| Security and privacy | | | |
| Performance and scale | | | |
| Operability | | | |
| Testability | | | |
| Evolvability | | | |

## Alignment Map

| Governing decision | As-built evidence | Status | Consequence | Reconciliation |
| --- | --- | --- | --- | --- |
| <decision> | <implementation path> | <aligned/intentional exception/implementation drift/architecture drift/unresolved> | <impact and blast radius> | <change implementation/update decision/govern exception/investigate> |

## Systemic Strengths

| Property | Evidence | Value to preserve |
| --- | --- | --- |
| <strength> | <evidence> | <leverage/locality/reliability/change value> |

## Systemic Risks

| Priority | Causal cluster | Evidence | Consequence and trigger | Scope |
| --- | --- | --- | --- | --- |
| <high/medium/low> | <architectural property> | <paths> | <current harm or future pressure> | <owners/features> |

## Recommended Direction

### Preserve

- <valuable property>

### Clarify or correct locally

- <proportionate action>

### Deepen or reshape

- <systemic change, trigger, and property to preserve>

### Investigate

- <unknown and cheapest discriminating observation>

## Confidence and Open Questions

- **Confirmed:**
- **Inferred:**
- **Unknown:**
```
