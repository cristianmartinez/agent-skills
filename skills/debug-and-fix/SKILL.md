---
name: debug-and-fix
description: Diagnose and fix software bugs and regressions with a compact symptom/where/after-what intake, evidence-driven reproduction, root-cause isolation, an explicit local-versus-architectural fix decision, and focused verification. Use when something is broken, failing, throwing, flaky, incorrect, or unexpectedly slow. For diagnosis-only requests, identify the cause and stop before editing.
license: MIT
---

# Debug and Fix

Resolve the reported failure with the fewest useful investigation loops. Optimize for evidence gained per token and tool call, without trading away correctness.

## 1. Frame the incident

Always begin by resolving these facts:

```text
Problem   What does the user observe, and what should happen instead?
Where     In which product surface, component, environment, input, or version?
After     After which action, change, deployment, upgrade, or point in time?
Pattern   Always, intermittently, or under specific conditions?
Evidence  Exact error, output, trace, screenshot, or minimal example already available?
```

Extract answers already present in the request or environment. Do not ask for them again. If a material field is missing and cannot be discovered, ask one compact intake question containing only the missing fields. Accept partial answers and unsolicited context.

State the resulting incident frame in at most five short lines. Label assumptions.

Respect the requested scope:

- **Diagnose/debug:** establish the cause and supporting evidence; propose a fix without editing.
- **Fix/resolve/make it work:** diagnose, implement, and verify the fix.

## 2. Find the tightest signal

Choose the cheapest signal that can distinguish the reported failure from success:

- Existing focused test or command
- Minimal reproduction using the reported input
- Targeted log, trace, debugger observation, or query
- Differential comparison with a known-good version, environment, or input
- Repeated or stress run for intermittent failures

Prefer an existing signal. Create a regression test or harness when it materially improves confidence or protects the fix. A useful signal exercises the real path and can fail for the user's exact symptom.

If reproduction is unsafe, inaccessible, or production-only, collect the smallest redacted evidence that can discriminate causes. Never expose credentials, tokens, personal data, auth headers, or unrelated logs.

Read [references/hard-cases.md](references/hard-cases.md) only for intermittent, performance, UI, distributed, environment-specific, or production-only failures.

## 3. Narrow by information gain

Trace backward from the symptom to the first incorrect state or boundary. Inspect recent changes suggested by **After** before searching the whole codebase.

Maintain a small ranked set of falsifiable hypotheses. Test the probe most likely to separate them. Change one explanatory variable at a time.

After each probe, ask:

```text
What did this rule out, confirm, or make more likely?
```

Discard observations that do not change the next decision. Expand scope only when narrower evidence fails.

## 4. Control token and tool cost

- Search symbols, errors, and affected paths before opening large files.
- Read the smallest complete unit needed to understand behavior.
- Filter command output at the source; quote only signal-bearing lines.
- Summarize repeated evidence instead of replaying it.
- Do not rerun an unchanged command unless repetition tests nondeterminism.
- Prefer one discriminating probe over broad logging.
- Keep the incident frame and current leading cause, not a transcript of discarded theories.
- Stop searching when additional evidence is unlikely to change the fix or confidence.

Token efficiency is subordinate to root-cause evidence and adequate verification.

## 5. Establish the cause

A root cause explains:

```text
trigger → incorrect state or violated invariant → observed symptom
```

Demonstrate the causal link with a reproduction, code path, measurement, controlled comparison, or other direct evidence. A plausible location, nearby error, or recently changed file is not yet a cause.

If the evidence remains ambiguous, report the leading explanation, alternatives still alive, and the smallest missing observation. Do not manufacture certainty.

## 6. Decide the fix depth

Classify the problem only after establishing the causal mechanism. Do not infer solution depth from the size, urgency, or visibility of the symptom.

Record the cause class, selected response, and evidence connecting them. Containment is a temporary response, not a cause class.

Use these distinctions:

- **Local implementation defect:** The existing ownership and contract are sufficient to enforce the invariant; the implementation violates them. Repair the implementation.
- **Weak existing boundary:** The correct module owns the behavior, but its contract or guarantees must change to prevent the diagnosed failure. Strengthen that boundary.
- **Architectural defect:** Responsibility, representation, or the necessary primitive is missing or incorrectly placed. Repair the shared design and migrate affected callers rather than adding a symptom-site exception.
- **Containment:** An urgent, reversible measure restores operation without removing the cause. Label it temporary, state its limitations and removal condition, and do not present it as the completed fix.

Choose the least extensive response that fully prevents the diagnosed failure. Architectural repair requires evidence that implementation or contract changes within the existing owner are insufficient.

Treat these as architectural signals, not automatic proof:

- The same rule or failure exists across multiple callers or components.
- Policy, state, or validation is duplicated and can diverge.
- Correctness depends on every caller following an undocumented convention.
- The apparent patch requires a special case at the symptom site instead of the owning boundary.
- Ownership is ambiguous, or no module can enforce the invariant.
- A focused regression test is impossible because the behavior has no usable seam.
- A local patch would leave multiple sources of truth, hidden coupling, or the same failure path elsewhere.

Confirm architectural scope with code-path evidence before expanding the change. A one-line symptom can reveal an architectural defect; a broad mechanical migration can still implement a simple, well-contained correction.

Keep urgency separate from solution depth. When immediate containment is necessary, verify it independently and preserve the diagnosed durable repair as explicit remaining work. Do not ask the user to choose “quick” or “proper” before the evidence supports the tradeoff.

## 7. Apply the smallest coherent fix

When authorized to fix, apply the response selected above. Repair the violated invariant at its responsible boundary. Prefer an existing abstraction over a symptom-specific conditional. Choose the smallest coherent fix, not merely the smallest diff. Keep unrelated cleanup outside the patch unless it is required to make the fix correct or testable.

If the durable repair would materially expand the user's requested scope, explain the evidence, proposed boundary change, and consequences before making that expansion. A normal repair within the affected system does not require separate permission merely because it touches several files.

Before editing, identify:

- The behavior that must change
- The behavior that must remain unchanged
- The verification that would reject a wrong fix

Remove temporary instrumentation and throwaway artifacts before completion.

## 8. Verify the outcome

Run the original signal against the original scenario. Then run the smallest relevant regression checks for the affected boundary.

Completion requires:

- The original symptom is reproduced or otherwise evidenced before the fix when practicable
- The causal mechanism is identified with evidence
- The fix-depth classification follows from that mechanism
- The original scenario succeeds after the fix
- A targeted regression check passes, or the absence of a valid test seam is explained
- Relevant nearby behavior remains intact
- Temporary diagnostics are removed

Broaden validation only when blast radius, uncertainty, or repository rules justify it.

## Final response

Keep the handoff compact:

```text
Class: <local implementation defect, weak boundary, or architectural defect>
Cause: <causal chain>
Decision: <why this response depth is appropriate>
Fix: <what changed, if authorized, including containment versus durable repair>
Proof: <reproduction and focused validation>
Residual: <remaining uncertainty or “none known”>
```

Include commands or file references only when they help the user reproduce, review, or continue the work.
