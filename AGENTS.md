# Skill maintenance

- Keep launcher-preference guidance repository-local by default. Do not modify a user's global Codex, Claude, Copilot, or other agent instructions unless the user explicitly requests a global policy.
- When applying or testing this skill against a project, prefer that project's supported automatic launcher over direct Docker Compose startup.
- Keep the packaged skill under `skills/local-docker-port-resolver` valid with the Codex, Agent Skills reference, and GitHub Skill publisher validators before release.
