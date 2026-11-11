<div align="center">
  <h1>Agent Skills</h1>

  <p>Reusable AI agent skills to automate repetitive tasks and simplify my development workflow.</p>

  <p>
    <a href="#skills">Skills</a> ·
    <a href="#using-the-skills">Using the skills</a> ·
    <a href="#want-to-contribute">Want to contribute?</a>
  </p>

  <p>
    <a href="#skills"><img src="https://img.shields.io/badge/Skills-1-blue" alt="1 skill" /></a>
    <a href="LICENSE"><img src="https://img.shields.io/github/license/simonesiega/agent-skills" alt="License" /></a>
  </p>
</div>

## What's this?

Nothing fancy. This is where I keep the AI agent skills I use across my projects. Having them in one place makes it easier to reuse instructions, improve them, and find them again later.

It's mostly for my own workflow, but if you find something useful, feel free to take it and make it yours.

## Skills

| Skill | What it's for | Example prompts |
| --- | --- | --- |
| [Commit](skills/commit-skill/SKILL.md) | Review changes and recent history, then create a focused conventional Git commit when asked. | [View prompts](skills/commit-skill/PROMPT.md) |

I'll add more as I need them.

## How it's organized

Each skill has its own folder under `skills/`, with a `SKILL.md` explaining what it does and when to use it. Some also have a `PROMPT.md` with examples or other supporting files.

## Using the skills

Pick one that fits what you're doing, copy it into your own setup, and change anything you need. Different agents may look for skills in different places, so check the instructions for the tool you're using.

Here are some common locations. Copy the entire skill folder (for example, `commit-skill/`) into the appropriate directory:

| Agent | Project skills | Personal skills |
| --- | --- | --- |
| [Codex](https://learn.chatgpt.com/docs/build-skills) | `.agents/skills/` | `~/.agents/skills/` |
| [Claude Code](https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview) | `.claude/skills/` | `~/.claude/skills/` |
| [Cursor](https://prod.cursor.com/docs/skills) | `.cursor/skills/` | `~/.cursor/skills/` |
| [GitHub Copilot](https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/add-skills) | `.github/skills/` | `~/.copilot/skills/` |
| [Gemini CLI](https://geminicli.com/docs/cli/using-agent-skills/) | `.gemini/skills/` | `~/.gemini/skills/` |

Project paths are relative to the repository root; `~/` means your home directory.

There's nothing to install for this repository itself. It's just a collection of files you can browse and reuse.

## Want to contribute?

Found a mistake or have a way to make a skill more useful? Feel free to open an issue or a PR. Small fixes and suggestions are always welcome.

## License

This repository is licensed under the [MIT License](LICENSE).