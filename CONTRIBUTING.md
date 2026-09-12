# Contributing

Add each skill under `skills/<skill-name>/`. The directory name and the `name` in `SKILL.md` must match.

Start from `template/SKILL.template.md` when useful, rename the copied file to `SKILL.md`, and replace its placeholder name and description.

Every skill must contain:

```text
skills/<skill-name>/
└── SKILL.md
```

Add `references/`, `scripts/`, `assets/`, or client-specific metadata only when the skill needs them. Keep leaf skills self-contained so users can install them independently. A thin umbrella skill may compose explicitly named companion skills, but it must document the full bundle, detect unavailable companions, and stop at the affected phase boundary rather than silently duplicating or weakening their workflow.

Review instruction quality using the open [Agent Skills specification](https://agentskills.io/specification) and the context-load, information-hierarchy, completion-criterion, and pruning concepts in Matt Pocock's [`writing-for-agents`](https://github.com/mattpocock/skills/tree/main/skills/productivity/writing-for-agents). Treat these as decision criteria rather than mechanical line-count rules.

Before submitting a change:

1. Confirm the description says what the skill does and when it should activate.
2. Treat the description as an always-loaded context pointer: name each real trigger branch once and remove identity or synonyms that do not improve routing.
3. Keep the main file on the common execution path. Move branch-local criteria, delegation mechanics, schemas, and examples into directly linked references whose pointer states when to load them.
4. Give each step a checkable, appropriately demanding completion criterion. Remove no-op advice, duplicated rules, and facts the agent can cheaply inspect from the environment.
5. Prefer positive target behavior. Keep prohibitions for real boundaries or safety constraints and pair them with the behavior the agent should perform.
6. Verify every referenced path exists and remains inside the skill directory.
7. Validate the skill against the [Agent Skills specification](https://agentskills.io/specification).
8. Run `npx skills add . --list` from the repository root and confirm every intended skill appears exactly once.
9. Test installation for at least one supported agent with `npx skills add . --skill <name> --agent <agent>`.
10. Forward-test complex workflows with realistic inputs and observable behavior; tests that only match headings or wording do not establish reliability.

Use Conventional Commit headers such as `feat: add planning skill` or `fix: accept qualified answers`.
