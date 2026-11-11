---
name: commit-skill
description: Create a focused conventional Git commit only when explicitly requested. Inspect the changes and a bounded sample of commit history, choose an accurate type and scope, and add a commit body only if requested or approved when required.
---

# Commit

Use this skill **only when the user explicitly asks to create a commit**. Implementing, fixing, reviewing, suggesting a message, or preparing changes does not authorize committing. A commit request does not authorize pushing, merging, tagging, releasing, or rewriting history.

## Inspect

1. **Repository rules.** Read applicable instructions and required checks. The default here is a scoped conventional subject with no body. If repository requirements conflict with that **subject format, scope rule, body policy, or required trailers**, explain the conflict and obtain approval for a compatible message before committing. Follow higher-priority instructions; never silently bypass mandatory requirements.
2. **Working tree.** Verify that `HEAD` is on a branch. Inspect `git status --short --untracked-files=all`, `git diff`, `git diff --cached`, and relevant untracked files. Identify the user's intended change and preserve unrelated work, including existing staged changes. Stop and ask if scope is unclear, conflicts are unresolved, or a merge, rebase, cherry-pick, or revert is in progress. Never make an empty commit by default. Exclude secrets and unintended generated artifacts; do not disclose secret values.
3. **Recent history.** Read at most **15 recent subjects** with `git log -15 --format=%s`. If the affected area's scope remains unclear, read at most **10 additional subjects total** for relevant paths with `git log -10 --format=%s -- <path>`. Do not inspect the full history. An unborn branch has no history; report other unexpected Git errors. If history is unhelpful, infer the scope from the files.

## Commit message

Use this format unless a higher-priority instruction or an approved, mandatory repository requirement calls for another format:

```text
<type>(<scope>): <imperative summary>
```

For an actual compatibility-breaking change, add `!` after the scope: `feat(api)!: remove deprecated endpoint`. Make the break clear in the summary without inventing an unrequested body or footer.

Choose the **type** from what the change actually does:

| Type | Use when |
| --- | --- |
| `feat` | Adding a user-facing or developer-facing capability. |
| `fix` | Correcting a bug or incorrect behavior. |
| `refactor` | Restructuring code without changing intended behavior. |
| `perf` | Improving runtime performance. |
| `docs` | Changing documentation only. |
| `test` | Adding or updating tests without changing production behavior. |
| `build` | Changing dependencies, build systems, or packaging. |
| `ci` | Changing CI workflows or CI configuration. |
| `style` | Changing formatting only, without functional changes. |
| `chore` | Performing maintenance not better described by another type. |
| `revert` | Reverting a previous change. |

The **scope is required by default**. Derive it from the primary affected component or directory, informed by relevant history rather than the most recent commit alone. Reuse an accurate existing scope, or choose a short, lowercase kebab-case name. Use `repo` for genuinely repository-wide work. Do not imitate inconsistent historical formatting.

Keep the **summary** specific, concise, imperative (`add`, `fix`, `remove`), and initially lowercase, with no trailing period. Prefer **72 characters or fewer** for the whole subject. One commit should describe one coherent change.

### Good examples

| Message | Why it works |
| --- | --- |
| `feat(ui): add keyboard shortcuts` | `feat` introduces a capability; `ui` identifies the area; the summary says what was added. |
| `fix(auth): handle expired sessions` | `fix` corrects behavior; `auth` identifies the area; the summary names the case handled. |
| `refactor(api): simplify request validation` | `refactor` signals an internal change without intended behavior changes; the scope and goal are clear. |
| `docs(readme): explain local installation` | `docs` fits a documentation-only change; the scope and summary identify the file and topic. |
| `test(parser): cover malformed input` | `test` fits a test-only change; the scope and summary identify missing coverage. |
| `build(deps): update TypeScript dependency` | `build` fits dependency maintenance; `deps` identifies the area and the summary names what changed. |
| `ci(actions): cache build dependencies` | `ci` identifies a pipeline change; `actions` names the system and the summary describes the improvement. |
| `chore(repo): update ignore rules` | `chore` fits housekeeping; `repo` is an appropriate broad scope and the summary states the work. |

These examples are good **only when the actual diff matches them**. Correct syntax cannot make an inaccurate message useful.

### Bad examples

| Message | Problem |
| --- | --- |
| `Updated stuff` | Missing type and scope; vague and not imperative. |
| `feat: add keyboard shortcuts` | Missing required scope. |
| `fix(auth): Fixed the login bug.` | Past tense, uppercase initial, vague wording, and trailing period. |
| `chore(ui): add keyboard shortcuts` | A new capability belongs under `feat`. |
| `feat(UI): add keyboard shortcuts` | Scope should be lowercase. |
| `feat(ui): changes` | Summary does not describe the change. |

## Stage and validate

1. **Select only the intended changes.** If unrelated changes are already staged, stop and ask the user to isolate them; do not unstage, stash, discard, or include them. Otherwise stage only reviewed paths with `git add -- <path>...`. For a mixed file, stage only the intended hunks. Use `git add -p -- <path>` **only if interactive staging is supported**; otherwise use a safe, reviewable noninteractive method or stop and ask. Never stage the whole mixed file as a shortcut. Never use `git add .`, `git add -A`, or `git commit -a`.
2. **Staged-only requests.** If explicitly asked to commit only staged changes, keep the index selection **unchanged**: do not stage or unstage anything. Do not change existing unstaged or untracked work. This rule concerns both what enters the commit and preserving the user's other work; read-only checks and incidental ignored temporary caches are acceptable, but skip or seek approval for checks that could change that work.
3. **Checks.** Run relevant available checks, including required repository checks. Do not intentionally modify tracked project files or existing untracked work. Avoid automatic fixes, write-mode formatters, and code generation without explicit authorization. If a mandatory check needs to modify files, explain and ask; do not bypass it. Report unavailable, skipped, or failed checks. Do not commit after a failing check without explicit approval. If a check unexpectedly changes files, inspect and report the changes; do not silently stage them.
4. **Final index review.** Inspect `git diff --cached`, `git diff --cached --check`, and `git status --short` immediately before the commit. The staged diff must be nonempty, contain exactly the intended changes, and match the message. Stop on whitespace errors unless the user approves proceeding or separately authorizes a fix. Do not edit source files as part of a commit-only request. If checks inspected the working tree rather than a partially staged snapshot, disclose that limitation.

## Commit body: only on request

**Default: subject line only.** Do not add a description, bullets, footer, issue-closing text, or co-author trailer just because previous commits contain them.

Add a body **only if the user explicitly requests a commit description or multi-line message**, or approves one to satisfy mandatory repository requirements. Separate it from the subject with a blank line. Use supplied text when provided; otherwise briefly explain the change or rationale without repeating the subject or inventing claims. Reporting changes in chat is **not** permission to add a commit body. Add trailers only when requested or approved as mandatory; never bypass signing or message requirements.

Without a requested body:

```text
fix(auth): handle expired sessions
```

With an explicitly requested body:

```text
fix(auth): handle expired sessions

Reject expired tokens before loading account data.
Keep the existing response for valid sessions.
```

## Create and verify

Create **one new commit** containing only the reviewed changes with `git commit -m '<subject>'`. Use a second `-m` for the body **only when explicitly requested or approved to satisfy mandatory repository requirements**. Quote arguments safely for the active shell so message text remains literal. Do not amend, bypass hooks or signing requirements, or change Git configuration or identity to make the commit succeed.

If committing fails, inspect the error, Git status, and diffs before retrying: hooks may have changed files. Do not retry blindly. If a commit succeeds but verification detects a problem, report it and ask before amending or creating another commit.

Verify with `git log -1 --format=%H%n%B`, `git show --format= HEAD`, and `git status --short`. Check that the committed content and full message match the reviewed snapshot, including any hook-added trailers or body. Report unexpected changes rather than silently accepting or rewriting them. Report the hash, exact subject, checks performed (including failures and limitations), and remaining changes. **Never push unless separately requested.**