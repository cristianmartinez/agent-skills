# Feature Ledger

Keep this compact and adapt it to the working medium. It may live in the conversation for small features or in a durable artifact for substantial work.

```markdown
# <Feature> — Lifecycle Ledger

Terminal scope: <definition | architecture | planning | implementation>

## Phase state
| Phase | Status | Gate evidence | Stale because |
| --- | --- | --- | --- |
| Definition | not-started | | |
| Architecture | not-started | | |
| Planning | not-started | | |
| Implementation | not-started | | |

## Decisions
| ID | Phase | Decision | Status | Provenance | Depends on | Affects |
| --- | --- | --- | --- | --- | --- | --- |

## Unresolved and deferred
| ID | Consequence | Owner | Forcing event | Current assumption |
| --- | --- | --- | --- | --- |

## Artifact handoffs
| From → To | Artifact or evidence | Confirmed at |
| --- | --- | --- |
```

## Propagation rules

- A direct correction creates a new decision and marks the old one `superseded`; do not rewrite history invisibly.
- Mark downstream work `stale` only when it depends on the changed decision.
- Revalidate stale gates in dependency order and keep unaffected work complete.
- Repository evidence can disprove an inference but cannot override a confirmed product judgment without returning the conflict to the user.
- Delegated analysis contributes evidence; the coordinating agent owns the accepted decision.
