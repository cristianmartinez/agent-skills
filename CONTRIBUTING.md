# Contributing

Add each skill under `skills/<skill-name>/`. The directory name and the `name` in `SKILL.md` must match.

Start from `template/SKILL.template.md` when useful, rename the copied file to `SKILL.md`, and replace its placeholder name and description.

Every skill must contain:

```text
skills/<skill-name>/
└── SKILL.md
```

Add `references/`, `scripts/`, `assets/`, or client-specific metadata only when the skill needs them. Keep each skill self-contained so users can install it independently.

Before submitting a change:

1. Confirm the description says what the skill does and when it should activate.
2. Keep the main instructions focused; move conditional detail into directly linked references.
3. Verify every referenced path exists and remains inside the skill directory.
4. Validate the skill against the [Agent Skills specification](https://agentskills.io/specification).
5. Run `npx skills add . --list` from the repository root and confirm every intended skill appears exactly once.
6. Test installation for at least one supported agent with `npx skills add . --skill <name> --agent <agent>`.

Use Conventional Commit headers such as `feat: add planning skill` or `fix: accept qualified answers`.
