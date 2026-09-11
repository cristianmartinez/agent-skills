# Hard-case debugging

Load only the applicable section. Return to the core workflow once the failure has a discriminating signal.

## Intermittent and timing-sensitive failures

- Increase the reproduction rate with controlled repetition, concurrency, load, or scheduling pressure.
- Pin random seeds, clocks, locale, time zone, resource limits, and dependency versions where relevant.
- Record successes and failures separately; compare the earliest divergent state.
- Prefer event ordering, state-transition, and ownership evidence over added sleeps.
- Treat a stable high reproduction rate as a useful signal even when individual runs remain nondeterministic.

## Performance regressions

- Define the user-visible regression and representative workload before profiling.
- Compare the same workload, environment, warmup, and sample method.
- Measure before changing code; use profilers, traces, query plans, or structural counters rather than verbose hot-path logging.
- Inspect the **After** change vector and compare known-good versus failing revisions when possible.
- Check latency distribution, resource use, allocations, and correctness guardrails; a faster but semantically different path is not a fix.

## UI and interaction failures

- Capture the exact route, viewport, input sequence, state, and browser or device.
- Inspect DOM or accessibility state, console, network, and screenshots only as needed to separate rendering, state, event, and backend causes.
- Reproduce the user's interaction rather than judging a static screenshot when behavior is the issue.
- Verify loading, error, empty, cancellation, focus, keyboard, and responsive states affected by the fix.

## Distributed and asynchronous failures

- Follow one request, job, or event across boundaries using correlation identifiers and timestamps.
- Check contracts at each boundary: payload, ordering, retries, idempotency, timeout, cancellation, and ownership.
- Distinguish delayed, duplicated, dropped, and incorrectly processed work.
- Prefer a trace of one failing transaction over aggregate logs from the whole system.

## Environment-specific failures

- Compare configuration, dependency versions, platform, feature flags, permissions, data shape, and external-service behavior.
- Change one environmental difference at a time.
- Reproduce in the closest safe environment; do not silently “fix” the test environment while production remains different.

## Production-only failures

- Use already-authorized read-only telemetry first.
- Redact secrets and personal data before displaying or persisting evidence.
- Propose minimal temporary instrumentation with a removal condition when existing evidence cannot distinguish causes.
- Keep operational mitigation separate from root-cause repair, and report both when an immediate mitigation is necessary.
