# My personal plugins for LLM harnesses

## Conventions

- In templates, placeholders MUST be written in parentheses, whether they stand for a value or for a passage of text (e.g., `# (System) threat model`, `(What the model covers, and what it leaves out.)`).
- In skills, only `SKILL.md` MAY link to the skill's other files (e.g., reference files, templates), so that every relative path resolves from the skill's root. Any other file MAY refer to them by name instead (e.g., "the report template").
- Skills and agents MUST refer to a skill by its bare name in their instructions (e.g., the `escalation` skill), since the slash and the plugin prefix (e.g., `/sdlc:escalation`) are specific to Claude Code.
- When adding a plugin, you MUST add its `skills` directory to `pi.skills` in `package.json`, so that Pi installs its skills too.
