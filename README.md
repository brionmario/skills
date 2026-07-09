# Skills

Brion Mario's personal collection of [Claude Code](https://code.claude.com) skills, packaged as a plugin marketplace.

## Install

```
/plugin marketplace add brionmario/skills
/plugin install brion-skills@brion-skills
```

Or, for local development:

```
claude --plugin-dir /path/to/skills
```

## Skills

- **create-presentation** — Generate single-file HTML slide presentations with Brion Mario's portfolio design language.
- **thunderid-create-dx-task** — Create a Developer Experience GitHub issue in the `thunder-id/thunderid` repo.

## Adding a new skill

1. Create a folder under `skills/<skill-name>/` with a `SKILL.md` (frontmatter needs `name` and `description`).
2. Run `claude --plugin-dir .` to test it locally, then `/reload-plugins` after changes.
3. Bump the `version` in `.claude-plugin/plugin.json` before pushing a release.
