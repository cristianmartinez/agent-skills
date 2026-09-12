# Parallel Architecture Assessment

Use this only when a broad or consequential assessment earns independent passes.

## Independent passes

- **Governance analyst:** Extract governing decisions, rationale, scope, status, and conflicts from product contracts, architecture documents, ADRs, and repository rules. Compare implementation only where needed to identify alignment questions.
- **As-built cartographer:** Trace representative success and failure paths; map owners, interfaces, dependencies, state, external systems, and operational controls from runtime evidence.
- **Architecture evaluator:** Assess the applicable criteria and systemic pressures from raw code, tests, history, and runtime evidence without seeing the other passes' conclusions.

Give each pass the same target and scope plus only its raw sources. Require confirmed facts, inferences, unknowns, and evidence → property → consequence chains. Keep every pass read-only and parallelize independent work rather than dependent reasoning.

Use available worker slots; the coordinator may own one pass and sequence the remainder. When model routing is supported and authorized, use fast capable models for bounded inventory and path tracing, strong reasoning for criteria evaluation, and the strongest permitted reasoning for alignment, drift, and synthesis. Otherwise use the current permitted model.

The coordinator inspects decisive evidence, reconciles contradictions, and synthesizes after every pass finishes. Agent agreement is a hypothesis, not proof. Preserve material conflicts as unresolved and name the cheapest discriminating observation.
