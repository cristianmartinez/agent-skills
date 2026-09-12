# Architecture Decision Template

Use this structure when the user wants a durable design artifact. Omit sections that genuinely do not apply; preserve the distinctions between evidence, decisions, and uncertainty.

```markdown
# <Feature> — Solution Architecture

Status: proposed

## Feature Contract

- **Problem:**
- **Actors:**
- **Required outcomes:**
- **First slice:**
- **Constraints:**
- **Non-goals:**

## Decision Ledger

Reference the lifecycle ledger when one exists; otherwise preserve the relevant decisions here.

| Decision | Status | Provenance | Depends on / affects |
| --- | --- | --- | --- |

## Evidence and Current System

| Source | Confirmed fact | Relevance |
| --- | --- | --- |
| `<path, contract, trace, or test>` | <fact> | <why it governs the design> |

Describe the representative current flow, source of truth, identity model, interfaces, invariants, and failure behavior. Label architectural inference.

## Concept and Ownership Map

| Product concept or operation | Owning module | Interface and guarantee | Source of truth | State or failure notes |
| --- | --- | --- | --- | --- |
| <concept> | <owner> | <caller-visible contract> | <authority> | <transitions/errors> |

## Proposed Flow

Describe the end-to-end control and data flow. Include persistence and external crossings only when relevant.

## Capability Decisions

| Capability | Decision | Rationale | Existing-path disposition |
| --- | --- | --- | --- |
| <capability> | <reuse/deepen/introduce/replace/defer> | <evidence> | <remain/adapt/migrate/deprecate/remove> |

## Interfaces and Invariants

- `<interface>` guarantees <behavior> and owns <invariant>.
- Callers may assume <contract>.
- The module must not depend on or duplicate <forbidden knowledge/state>.

## Options Considered

### Recommended — <option>

- **Fit:**
- **Accepted tradeoff:**
- **Evidence:**
- **Reversal condition:**

### Rejected — <option>

- **Why viable:**
- **Why rejected:**

## Migration and Compatibility

State coexistence rules, data migration, rollout, rollback, and deletion conditions. Name any temporary compatibility path and its removal trigger.

## Risks and Proofs

| Unknown or risk | Consequence | Proof checkpoint | Design response if disproven |
| --- | --- | --- | --- |
| <risk> | <impact> | <test/spike/trace/benchmark/review> | <change> |

## Execution Handoff

- **Architectural sequence:** <dependency order without task-level decomposition>
- **First proof gate:**
- **Migration/deletion gate:**
- **No-duplicate-path constraint:**
- **Planning inputs:** <decisions the execution planner must preserve>

## Open Decisions

### Product decisions

- <unresolved judgment and consequence>

### Technical unknowns

- <unknown, proof, and consequence>
```
