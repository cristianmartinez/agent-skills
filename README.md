# Product Definition

[![skills.sh](https://skills.sh/b/cristianmartinez/product-definition)](https://skills.sh/cristianmartinez/product-definition/product-definition)

An interactive Agent Skill that uncovers product blind spots through short decision rounds, then synthesizes the result into a rigorous Product Definition.

## Portable by design

The portable skill is [`SKILL.md`](SKILL.md) plus its [`references/`](references/) directory. This follows the open [Agent Skills specification](https://agentskills.io/specification) and can be used by compatible agents without maintaining separate prompt copies.

[`agents/openai.yaml`](agents/openai.yaml) contains optional Codex interface metadata. It does not replace or modify the portable instructions, and other agents can ignore it.

## Install

Let the CLI detect or prompt for your agent:

```bash
npx skills add cristianmartinez/product-definition --skill product-definition
```

Install for a particular agent:

```bash
# Claude Code
npx skills add cristianmartinez/product-definition --skill product-definition --agent claude-code

# Codex
npx skills add cristianmartinez/product-definition --skill product-definition --agent codex

# Cursor
npx skills add cristianmartinez/product-definition --skill product-definition --agent cursor

# Gemini CLI
npx skills add cristianmartinez/product-definition --skill product-definition --agent gemini-cli

# GitHub Copilot
npx skills add cristianmartinez/product-definition --skill product-definition --agent github-copilot
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
