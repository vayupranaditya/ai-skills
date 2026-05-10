# Convert Skill Prompt

Use this prompt when converting a canonical skill from `core/*.skill.md` into the IDE-specific formats in this repository.

```text
You are converting one canonical AI skill into all supported IDE targets in this repo.

Source skill:
- Path: <core/<skill_slug>.skill.md>

Supported targets:
- Codex: ide/codex/skills/<skill-slug>/SKILL.md
- Claude Code: ide/claude-code/.claude/skills/<skill-slug>/SKILL.md
- Kiro: ide/kiro/steerings/<skill-slug>.md
- Antigravity: ide/antigravity/<SKILL_NAME>.AGENTS.md

Conversion rules:
1. Read the source skill completely before editing.
2. Derive a stable kebab-case <skill-slug> from the title or source filename.
3. Preserve the original meaning, constraints, response style, and examples.
4. Do not invent new behavior, tools, guarantees, or external dependencies.
5. Adapt only the wrapper metadata and heading depth needed by each IDE.
6. Keep wording concise and instruction-oriented.

Codex output:
- Create ide/codex/skills/<skill-slug>/SKILL.md.
- Use YAML frontmatter with:
  - name: <skill-slug>
  - description: <clear activation description, including when to use the skill>
- Put the converted instructions in Markdown after the frontmatter.

Claude Code output:
- Create ide/claude-code/.claude/skills/<skill-slug>/SKILL.md.
- Use YAML frontmatter with:
  - name: <human-readable skill name>
  - description: <clear activation description, including when to use the skill>
- Put the converted instructions in Markdown after the frontmatter.

Kiro output:
- Create ide/kiro/steerings/<skill-slug>.md.
- Use YAML frontmatter with:
  - inclusion: auto
  - name: <skill-slug>
  - description: <clear activation description, including when to use the steering>
- Put the converted steering content in Markdown after the frontmatter.
- Keep the file suitable to copy into a Kiro workspace under .kiro/steering/<skill-slug>.md.

Antigravity output:
- Create or update ide/antigravity/<SKILL_NAME>.AGENTS.md, where <SKILL_NAME> is the uppercase underscore form of the source skill name.
- Keep the file as plain Markdown.
- Name the top-level section after the skill title.
- Include a one-paragraph activation statement before the full behavior instructions.
- Keep the file suitable to copy or merge into a project-level agent rules file.

Validation:
- Confirm all target files exist.
- Confirm Codex, Claude Code, and Kiro files start with valid YAML frontmatter.
- Confirm Antigravity *.AGENTS.md remains plain Markdown.
- Confirm no target mentions unsupported IDE-specific capabilities.
```
