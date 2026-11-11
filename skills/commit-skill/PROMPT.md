
# Commit prompts

[← Commit skill](SKILL.md)

Here are a few prompts I use with `$commit-skill`. It checks the changes and a small sample of recent commit history to choose the type, scope, and summary, so I usually don't need to specify those myself.

Replace anything in `<angle brackets>` with your own details. They're placeholders in the prompt, not command-line options.

## Commit the current work

```text
$commit-skill Commit the current changes.
```

The usual case. The agent checks what's changed, runs relevant checks, and makes a single-line commit. If the intended changes aren't clear, it asks before including unrelated work.

## Commit specific files

```text
$commit-skill Commit only <files-or-directories>. Leave everything else untouched.
```

Useful when the working tree contains other changes you don't want in the commit.

## Commit one change

```text
$commit-skill Commit only <change-or-feature>. Don't include <unrelated-change>.
```

You don't have to list every affected file. The agent should identify the relevant changes and keep the commit focused.

## Commit staged changes only

```text
$commit-skill Commit only the changes already staged. Leave all unstaged and untracked changes untouched.
```

Useful when you've already selected the exact changes. The agent keeps the index selection unchanged and avoids checks that could modify your other work.

## Include a description

```text
$commit-skill Commit <change-or-files> and add a short commit body explaining why the change was needed.
```

This explicitly requests a description **inside the Git commit**. Without it, the skill uses a subject-only message by default.

## Provide the exact description

```text
$commit-skill Commit <change-or-files>. Use this exact commit body:

<commit-description>
```

Use this when you already know the body text. The agent still chooses the subject from the actual changes.

## Review without creating a commit

```text
Review <change-or-files> and suggest a conventional commit message, but don't stage or commit anything.
```

This is review-only, so it doesn't invoke `$commit-skill`: that skill is reserved for explicit requests to create a commit.