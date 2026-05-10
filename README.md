# ai-skills

Portable AI assistant skills for repeatable personal workflows.

This repository keeps each skill in a canonical Markdown form under `core/`, then publishes IDE-specific adaptations under `ide/`. The goal is to write a scenario once and keep it usable across the AI coding tools you actually work in.

## Repository Layout

```text
core/
  <skill-name>.skill.md

ide/
  codex/
    skills/
      <skill-name>/
        SKILL.md

  claude-code/
    .claude/
      skills/
        <skill-name>/
          SKILL.md

  kiro/
    steerings/
      <skill-name>.md

  antigravity/
    <SKILL_NAME>.AGENTS.md
```

## Canonical Skills

`core/*.skill.md` files are the source of truth. Keep them tool-neutral:

- describe the scenario and purpose
- define when the assistant should apply the skill
- list the behavioral rules
- include response style requirements
- avoid IDE-specific paths unless the skill itself is about that IDE

## IDE Targets

Codex and Claude Code use Agent Skills directories with a `SKILL.md` file and YAML frontmatter.

Kiro uses steering Markdown. Files in `ide/kiro/steerings/` are intended to be copied into `.kiro/steering/` when installed in a workspace.

Antigravity uses skill-specific `*.AGENTS.md` rules files. Files in `ide/antigravity/` are intended to be copied or merged into a project-level agent rules file as needed.

## Converting Skills

Use [CONVERT_SKILL_PROMPT.md](CONVERT_SKILL_PROMPT.md) to convert a canonical skill into all supported IDE targets.

The conversion should preserve the skill's intent and only adapt the file structure, frontmatter, and heading levels required by each IDE.

## Adding A Skill

1. Add the canonical skill to `core/<skill-name>.skill.md`.
2. Run the conversion prompt from [CONVERT_SKILL_PROMPT.md](CONVERT_SKILL_PROMPT.md).
3. Review every generated target file for drift from the canonical version.
4. Install only the target folder or file needed by the IDE you are using.

## Install Paths

```text
Codex:
  ide/codex/skills/<skill-name>/ -> ~/.codex/skills/<skill-name>/

Claude Code:
  ide/claude-code/.claude/skills/<skill-name>/ -> <project>/.claude/skills/<skill-name>/

Kiro:
  ide/kiro/steerings/<skill-name>.md -> <project>/.kiro/steering/<skill-name>.md

Antigravity:
  ide/antigravity/<SKILL_NAME>.AGENTS.md -> <project>/AGENTS.md or equivalent agent rules file
```

## Pre-Commit Guard

Install the tracked hook with:

```sh
scripts/setup-githooks.sh
```

The hook checks staged changes. When a canonical skill changes in `core/`, the matching IDE files must be staged in the same commit:

```text
core/<name>.skill.<ext>
ide/antigravity/<NAME>.AGENTS.md
ide/claude-code/.claude/skills/<name-with-dashes>/SKILL.md
ide/codex/skills/<name-with-dashes>/SKILL.md
ide/kiro/steerings/<name-with-dashes>.md
```

## Maintenance Rules

- Treat `core/` as the editable source.
- Regenerate IDE targets after changing a canonical skill.
- Keep each skill focused on one scenario.
- Prefer concrete behavioral rules over broad philosophy.
- Do not store secrets, private credentials, or environment-specific tokens in skills.
