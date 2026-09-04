---
name: thunderid-create-pr
description: Create a GitHub pull request in a ThunderID repo (any SDK repo, thunderid-sdk-components, skills, etc.), following that repo's own commit-message style and PR template. Use when asked to "create a PR", "open a pull request", "submit this as a PR", or "push this up" for a ThunderID repo.
allowed-tools: Bash(git *), Bash(gh pr create *), Bash(gh pr edit *), Bash(gh pr view *), Bash(gh api *), Bash(gh repo view *), AskUserQuestion
---

# ThunderID PR Creator

You are opening a pull request for a change already made in a ThunderID repo's working tree. This skill exists because ThunderID repos do **not** use Conventional Commits, and each repo has its own PR template that must be followed verbatim — generic "## Summary / ## Test plan" bodies are wrong here.

## Step 0 — Confirm you're in the right repo

Before doing anything, verify the working directory is actually one of the current ThunderID repos and not a stale clone:

```bash
git remote -v
```

- If the path contains `thunderid-workspace`, or the origin does not point at a `brionmario/*-sdks`, `brionmario/thunderid-*`, or `thunder-id/*` repo, stop and confirm with the user before proceeding.
- Note whether `origin` is a fork with a separate `upstream` remote (common for this user — e.g. `origin` = `brionmario/thunderid-skills`, `upstream` = `thunder-id/skills`). PRs should target `upstream`'s default branch, not `origin`'s.

## Step 1 — Match the repo's commit message style

**Never use Conventional Commits** (`fix:`, `feat:`, `chore(scope):`, etc.) unless the repo's own history genuinely uses that style. Check first:

```bash
git log --oneline -15
```

Write commit messages as plain, short, imperative sentences matching what you see (e.g. "Use automation bot PAT in release workflow instead of default GITHUB_TOKEN", "Fix skills repo url", "Update README"). No prefix, no scope, no em dashes or `--`.

If a commit already exists with the wrong style, amend it:

```bash
git commit --amend -m "<plain sentence, matching repo history>"
git push --force-with-lease
```

**Prefer a single commit per PR/branch.** Check `git log --oneline <default-branch>..HEAD` — if there's more
than one commit (or there are uncommitted changes on top), squash everything into one commit before pushing,
rather than leaving a multi-commit history:

```bash
git add -A
git reset --soft <default-branch>
git commit -m "<plain sentence>"
git push --force-with-lease
```

## Step 2 — Find and use the repo's actual PR template

Look for, in this priority order:

```bash
find . -maxdepth 2 -iname "pull_request_template.md"
```

1. `.github/pull_request_template.md` — this is the one GitHub actually auto-populates into new PRs; prefer it when both exist.
2. Root-level `pull_request_template.md` — fallback only.

Read the template and fill in **every section it defines**, in full prose (no leftover `<placeholder>` text, no invented sections). Do not use a generic Summary/Test-plan format — that is wrong for these repos.

**This is the most common way this skill goes wrong**: it's easy to default to a familiar `## Summary` /
`## Test plan` / `## What's included` body instead of stopping to read the actual template file first. Before
writing `--body`, always cat the template file (`.github/pull_request_template.md` etc.) in this session so
its exact headings are in front of you, then write the body using those exact `###` headings, in that order —
never substitute your own structure, even if it feels more natural or more complete. If you're editing an
*existing* PR (`gh pr edit`/`gh api ... PATCH`), fetch its current body first (`gh pr view <n> --json body` or
`gh api repos/<owner>/<repo>/pulls/<n> --jq .body`) — if it's already using a generic Summary/Test-plan format,
that's a bug to fix, not a format to preserve; rewrite it around the template's sections.

For the common ThunderID SDK template (ios/android/flutter/javascript-sdks/skills all share close variants of this), the sections are typically:

- `### Purpose` — the problem/feature/change, briefly
- `### Approach` — how it was implemented and key decisions
- `### Related Issues` — linked issue(s), or `- N/A`
- `### Related PRs` — linked PR(s), or `- N/A`
- `### Checklist` — check off what's actually true (contribution guidelines followed, manual testing done, docs provided, breaking changes section filled if applicable)
- `### Security checks` — check off what's actually true (secure coding standards followed, no secrets committed)

Only check a checklist box if it is actually true for this change — do not blanket-check everything.

## Step 3 — Preview and confirm

Show the user the exact title + filled-in body before creating anything. Use `AskUserQuestion` to confirm:

```
question: "Ready to open this PR?"
header: "Confirm"
options:
  - label: "Create it"
    description: "Push the branch and open the PR"
  - label: "Make changes"
    description: "I want to edit something first"
```

## Step 4 — Push and create

```bash
git push -u origin <branch>
gh pr create --title "<plain-sentence title>" --body "<filled template>"
```

If `origin` is a fork of an `upstream` repo, `gh pr create` should already target `upstream`'s default branch automatically — verify the printed PR URL points at the `upstream` org, and if not, pass `--repo <upstream-owner>/<upstream-repo>` explicitly.

### Known gotcha: `gh pr edit` GraphQL error

`gh pr edit` on these repos can fail with:

```
GraphQL: Projects (classic) is being deprecated in favor of the new Projects experience... (repository.pullRequest.projectCards)
```

This is unrelated to the actual edit and can silently no-op the title/body change. Verify the edit landed with `gh pr view <number> --json title,body`. If it didn't, fall back to the REST API directly, which does not hit this bug:

```bash
gh api repos/<owner>/<repo>/pulls/<number> -X PATCH -f title="<title>"
gh api repos/<owner>/<repo>/pulls/<number> -X PATCH -f body="<body>"
```

## Step 5 — Report

Output the final PR URL. Do not add a Claude/Anthropic co-author trailer to any commit or PR.
