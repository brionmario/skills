# Skills

[![Claude Code](https://img.shields.io/badge/Claude%20Code-D97757?logo=claude&logoColor=white)](https://code.claude.com)
[![Codex CLI](https://img.shields.io/badge/Codex%20CLI-000000?logo=openai&logoColor=white)](https://developers.openai.com/codex)
[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-open%20standard-6E56CF)](https://github.com/anthropics/skills)

Brion Mario's personal collection of [Agent Skills](https://github.com/anthropics/skills) — an open, portable format for packaging procedural knowledge that any compatible coding agent can load. This repo is also a [Claude Code plugin marketplace](https://code.claude.com/docs/en/plugin-marketplaces), so the same skills install as a single plugin there, or drop straight into any other Agent-Skills-compatible tool (Codex CLI, Cursor, GitHub Copilot, Gemini CLI, and others).

## Skills

- **create-presentation** — Generate single-file HTML slide presentations with Brion Mario's portfolio design language.
- **thunderid-create-dx-task** — Create a Developer Experience GitHub issue in the `thunder-id/thunderid` repo.

## Install

### Claude Code

Add the marketplace once, then install the plugin:

```
/plugin marketplace add brionmario/skills
/plugin install brion-skills@brion-skills
```

For local development, point Claude Code straight at your checkout instead:

```
claude --plugin-dir /path/to/skills
```

### Codex CLI

Codex reads skills from `~/.codex/skills` (global) or `.agents/skills` (per-repo). Clone this repo and symlink in the ones you want:

```
git clone https://github.com/brionmario/skills.git ~/dev/brion-skills
mkdir -p ~/.codex/skills
ln -s ~/dev/brion-skills/skills/*/ ~/.codex/skills/
```

Or, to scope a skill to a single project, symlink it into that project's `.agents/skills/` directory instead. Restart Codex if a newly linked skill doesn't show up.

### Other Agent Skills-compatible tools

Any tool that supports the [Agent Skills](https://github.com/anthropics/skills) open standard (Cursor, GitHub Copilot, Gemini CLI, VS Code, and 30+ others) reads the same `SKILL.md` format. Copy or symlink the relevant `skills/<skill-name>/` folder into wherever your tool looks for skills.

## Adding a new skill

1. Create a folder under `skills/<skill-name>/` with a `SKILL.md` (frontmatter needs `name` and `description`).
2. Run `claude --plugin-dir .` to test it locally in Claude Code, then `/reload-plugins` after changes.
3. Bump the `version` in `.claude-plugin/plugin.json` before pushing a release.
