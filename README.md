# Agent Skills

[![skills.sh](https://skills.sh/b/cristianmartinez/agent-skills)](https://skills.sh/cristianmartinez/agent-skills)

A collection of portable Agent Skills for product and software-development work.

## Skills

| Skill | Purpose |
|---|---|
| [`feature`](skills/feature/) | Orchestrate the complete Define → Architect → Plan → Implement lifecycle while preserving decisions and resuming from stale or incomplete gates. |
| [`product-definition`](skills/product-definition/) | Uncover product blind spots through short decision rounds, then synthesize a rigorous Product Definition. |
| [`solution-architecture`](skills/solution-architecture/) | Map a defined product or feature onto an existing system and produce an evidence-backed technical design before planning implementation. |
| [`feature-planning`](skills/feature-planning/) | Turn approved definition and architecture decisions into dependency-aware slices, model-routed task packets, and verification gates. |
| [`feature-implementation`](skills/feature-implementation/) | Implement an approved feature through coherent slices using complexity-matched models, explicit task packets, and verified integration. |
| [`architecture-assessment`](skills/architecture-assessment/) | Assess an as-built architecture against explicit criteria, including alignment, ownership, interfaces, state, resilience, and evolution. |
| [`feature-assessment`](skills/feature-assessment/) | Reverse-engineer an implemented feature and explain how it works, what is strong, what is flawed, and what should improve. |
| [`debug-and-fix`](skills/debug-and-fix/) | Diagnose failures, distinguish local defects from architectural problems after finding the cause, apply the right-depth repair, and verify the exact symptom efficiently. |

## Portable by design

Each directory under [`skills/`](skills/) is a self-contained skill. Its portable contract is `SKILL.md` plus any referenced resources. This follows the open [Agent Skills specification](https://agentskills.io/specification) and can be used by compatible agents without maintaining separate prompt copies.

Some skills include `agents/openai.yaml` for optional Codex interface metadata. It does not replace or modify the portable instructions, and other agents can ignore it.

## Install

Install the complete feature lifecycle:

```bash
npx skills add cristianmartinez/agent-skills \
  --skill feature \
  --skill product-definition \
  --skill solution-architecture \
  --skill feature-planning \
  --skill feature-implementation
```

The four phase skills remain independently useful. The `feature` skill is deliberately a thin orchestrator and needs those companions for full-fidelity end-to-end execution.

Install an individual skill and let the CLI detect or prompt for your agent:

```bash
npx skills add cristianmartinez/agent-skills --skill feature
npx skills add cristianmartinez/agent-skills --skill product-definition
npx skills add cristianmartinez/agent-skills --skill solution-architecture
npx skills add cristianmartinez/agent-skills --skill feature-planning
npx skills add cristianmartinez/agent-skills --skill feature-implementation
npx skills add cristianmartinez/agent-skills --skill architecture-assessment
npx skills add cristianmartinez/agent-skills --skill feature-assessment
npx skills add cristianmartinez/agent-skills --skill debug-and-fix
```

Install for a particular agent:

```bash
# Claude Code
npx skills add cristianmartinez/agent-skills --skill product-definition --agent claude-code

# Codex
npx skills add cristianmartinez/agent-skills --skill product-definition --agent codex

# Cursor
npx skills add cristianmartinez/agent-skills --skill product-definition --agent cursor

# Gemini CLI
npx skills add cristianmartinez/agent-skills --skill product-definition --agent gemini-cli

# GitHub Copilot
npx skills add cristianmartinez/agent-skills --skill product-definition --agent github-copilot
```

The [skills CLI](https://github.com/vercel-labs/skills) supports additional Agent Skills clients. Use `--agent '*'` to install for every locally supported agent.

## Use

Invoke the installed skill using the syntax supported by your agent, or ask it directly:

```text
Use product-definition to explore what I am not seeing and turn this idea into a product definition:

I need to build…
```

Answers can mix compact choices and additional context:

```text
1Y, but only for administrators
2=4 — automate only when the action is undoable
3N
4? Explain the consequences
Don't forget that this must work offline
```

The choices are shortcuts, not a restrictive form. Qualifiers, corrections, partial answers, and unsolicited constraints remain part of the product definition.

## Repository layout

```text
agent-skills/
├── skills/
│   └── <skill-name>/
│       ├── SKILL.md
│       ├── agents/          # Optional client-specific metadata
│       ├── references/      # Optional on-demand guidance
│       ├── scripts/         # Optional deterministic helpers
│       └── assets/          # Optional output resources
├── template/
│   └── SKILL.template.md
├── CONTRIBUTING.md
├── LICENSE
└── README.md
```

Phase and assessment skills must remain independently installable. An umbrella skill may compose explicitly named companion skills when it detects and reports missing companions instead of silently degrading or duplicating their instructions.
