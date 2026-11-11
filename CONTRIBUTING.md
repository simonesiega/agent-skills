# Contributing

[← Project README](README.md) · [Skills](README.md#skills)

Thanks for checking this out! This is mostly where I keep the agent skills I use myself, so contributions don't need to be anything big. A clearer instruction, a fixed example, or a useful new skill is more than enough.

## Quick version

1. Have a look at the existing [skills](README.md#skills) before adding something similar.
2. Keep your change focused. For a bigger idea, feel free to [open an issue](https://github.com/simonesiega/agent-skills/issues) first.
3. Put each new skill in its own folder under `skills/`.
4. Make sure the instructions and example prompts actually match what the skill does.
5. If you add or rename a skill, update the README's skills table and count badge.
6. Open a PR with a short explanation of what changed and why.

## Adding a skill

Each skill has a `SKILL.md` as its entry point:

```text
skills/
└── <skill-name>/
    ├── SKILL.md
    └── PROMPT.md       # optional examples
```

Use a short, lowercase, hyphenated folder name. Start `SKILL.md` with YAML frontmatter containing a `name` that matches the folder and a `description` explaining when the skill should be used.

I try to keep skills straightforward: say when to use one, what steps to follow, and what to avoid. Include examples when they make the instructions easier to understand. If a skill needs templates or other supporting files, keep them in the same folder and link to them from `SKILL.md`.

`PROMPT.md` is optional. If you add one, make the prompts easy to copy, use `<placeholders>` for details someone should replace, and keep the examples consistent with the skill's actual rules.

## Improving an existing skill

If something is confusing, too specific, or doesn't work as expected, feel free to improve it. Try to preserve the skill's original purpose and any important safeguards. If you're changing its behavior, explain why in the PR.

Please don't add secrets, personal project data, private files, or instructions that assume everyone uses the same agent or setup. Only claim compatibility you've actually checked.

## Before opening a PR

There's no special build or test setup for the collection right now. Just check that:

- The skill's folder, frontmatter name, and links agree.
- Any commands, examples, and paths make sense.
- `README.md` lists the available skills accurately, including the count badge.
- The change doesn't include unrelated files or local configuration.

For a small fix, a short PR description is fine. Mention what changed and, if relevant, how you tried it. I don't need a long write-up.

## One last thing

Questions and suggestions are welcome. If you spot something that could be better but don't feel like writing a PR, [open an issue](https://github.com/simonesiega/agent-skills/issues) instead.

Thanks for helping out!