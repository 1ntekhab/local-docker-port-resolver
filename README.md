# Local Docker Port Resolver

A portable [Agent Skill](https://agentskills.io) for preventing host-port collisions across local Docker Compose projects.

It inspects every enabled published service, selects available host ports without changing container ports, synchronizes public URLs and trusted origins, preserves optional profiles, and keeps actual production endpoints explicit.

## What it handles

- Multi-service Docker Compose stacks.
- Development and explicitly supported local-production simulations.
- Primary application edges, Mailpit, Grafana, debuggers, storage consoles, and other enabled published services.
- Strict named port overrides and bounded automatic fallback.
- Current-project mapping reuse and cross-service collision prevention.
- Backend origins, proxy redirects, frontend URLs, MFA/WebAuthn origins, E2E settings, and operational URLs.
- Secret-free resolved-port state for follow-up commands.

The skill is framework-neutral. It can adapt to Django, Next.js, Laravel, ASP.NET, Rails, Spring, Go, and other stacks after inspecting the repository.

## Agent compatibility

The core package follows the open Agent Skills `SKILL.md` format. It can be discovered by clients that implement that standard.

| Agent platform | Support | Notes |
|---|---|---|
| OpenAI Codex | Native | `agents/openai.yaml` adds Codex-specific UI metadata. |
| Claude Code | Native | Uses `SKILL.md` and the bundled reference directly. |
| GitHub Copilot | Native | Supported in VS Code, Copilot CLI, and the Copilot cloud agent. |
| Other Agent Skills clients | Format-compatible | Install in the skill directory documented by that client. |
| Agents without skills support | Manual instructions only | Provide `SKILL.md` as project context; automatic discovery is not guaranteed. |

The skill requires an agent with repository filesystem and shell access. Docker Compose is needed for rendered configuration and live conflict verification.

## Install

Review a third-party skill before installation, then clone this repository into the appropriate personal or project skill directory. The destination folder must remain named `local-docker-port-resolver` so it matches the `name` in `SKILL.md`.

| Platform | Personal installation | Project installation |
|---|---|---|
| OpenAI Codex | `~/.codex/skills/local-docker-port-resolver` | Use the project skill location supported by your Codex environment. |
| Claude Code | `~/.claude/skills/local-docker-port-resolver` | `.claude/skills/local-docker-port-resolver` |
| GitHub Copilot | `~/.copilot/skills/local-docker-port-resolver` | `.github/skills/local-docker-port-resolver` |
| Shared compatible location | `~/.agents/skills/local-docker-port-resolver` | `.agents/skills/local-docker-port-resolver` |

Example for Codex on Windows PowerShell:

```powershell
git clone https://github.com/1ntekhab/local-docker-port-resolver.git `
  "$env:USERPROFILE\.codex\skills\local-docker-port-resolver"
```

Example for Claude Code on macOS or Linux:

```bash
git clone https://github.com/1ntekhab/local-docker-port-resolver.git \
  ~/.claude/skills/local-docker-port-resolver
```

Example for a repository-shared GitHub Copilot skill:

```bash
git clone https://github.com/1ntekhab/local-docker-port-resolver.git \
  .github/skills/local-docker-port-resolver
```

Restart or open a new agent session if the installed skill is not discovered immediately.

## Use

Use a natural-language request that names the skill. Codex also supports the `$local-docker-port-resolver` form, while clients that expose skills as slash commands may use `/local-docker-port-resolver`.

```text
Use the Local Docker Port Resolver skill to add automatic host-port conflict resolution to this project's local Docker Compose stack.
```

To update an existing launcher after adding services:

```text
Use $local-docker-port-resolver to inspect the newly added Docker services and update the existing launcher, tests, and documentation.
```

## Safety boundary

Automatic fallback is for local development and explicitly supported local simulations. Live production should use stable public domains, explicit edge configuration, and private container networking rather than silently changing public ports.

## Skill contents

- `SKILL.md` contains the reusable workflow and constraints.
- `references/node-compose-pattern.md` contains the detailed Node.js and Docker Compose pattern.
- `agents/openai.yaml` supplies optional Codex UI metadata and the default prompt. Other agents can ignore it.

Only `SKILL.md` is required by the open format. The reference file is portable supporting material, and the `agents` directory is a product-specific enhancement.

## Standards and platform documentation

- [Agent Skills open standard](https://agentskills.io)
- [Anthropic: Agent Skills](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills)
- [GitHub Copilot and VS Code Agent Skills](https://code.visualstudio.com/docs/agent-customization/agent-skills)

## License

MIT
