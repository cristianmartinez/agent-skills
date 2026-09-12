# Parallel Feature Assessment

Use this only when the feature's breadth or consequence earns independent passes.

## Independent passes

- **Feature cartographer:** Reconstruct user flow, system flow, state, ownership, and relevant history without judging quality.
- **Product and lifecycle assessor:** Evaluate product coherence, failure and recovery, data lifecycle, user control, and meaningful limitations.
- **Engineering assessor:** Evaluate architecture, correctness, resilience, security, performance, operability, testability, and changeability.

Give each pass the same target and scope plus only its raw evidence locations. Withhold prior conclusions and expected findings. Require confirmed facts, inferences, unknowns, and evidence → property → consequence judgments. Keep every pass read-only and split by lens instead of sending duplicate broad prompts.

Use available worker slots; the coordinator may own one pass and sequence the remainder. When model routing is supported and authorized, use fast capable models for bounded discovery, strong reasoning for judgment-heavy lenses, and the strongest permitted reasoning for synthesis. Otherwise use the current permitted model.

The coordinator inspects decisive evidence, reconciles contradictions, deduplicates observations, and preserves distinct consequences after every pass finishes. Agent agreement is a hypothesis, not proof; keep material conflicts explicit.
