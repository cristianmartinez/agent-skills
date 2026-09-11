# Agent Skills

[![skills.sh](https://skills.sh/b/cristianmartinez/agent-skills)](https://skills.sh/cristianmartinez/agent-skills)

A collection of portable Agent Skills for product and software-development work.

## Skills

| Skill | Purpose |
|---|---|
| [`product-definition`](skills/product-definition/) | Uncover product blind spots through short decision rounds, then synthesize a rigorous Product Definition. |

## Portable by design

Each directory under [`skills/`](skills/) is a self-contained skill. Its portable contract is `SKILL.md` plus any referenced resources. This follows the open [Agent Skills specification](https://agentskills.io/specification) and can be used by compatible agents without maintaining separate prompt copies.

Some skills include `agents/openai.yaml` for optional Codex interface metadata. It does not replace or modify the portable instructions, and other agents can ignore it.

## Install

Let the CLI detect or prompt for your agent:

```bash
npx skills add cristianmartinez/agent-skills --skill product-definition
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

Skills must remain independently installable. Shared repository documentation may explain conventions, but one skill must not require another skill to be installed.
