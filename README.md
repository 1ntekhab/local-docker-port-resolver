# Local Docker Port Resolver

A reusable Codex skill for preventing host-port collisions across local Docker Compose projects.

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

## Install

Ask Codex to install the skill from this repository, or clone it into your personal Codex skills directory.

### Windows PowerShell

```powershell
git clone https://github.com/1ntekhab/local-docker-port-resolver.git `
  "$env:USERPROFILE\.codex\skills\local-docker-port-resolver"
```

### macOS or Linux

```bash
git clone https://github.com/1ntekhab/local-docker-port-resolver.git \
  ~/.codex/skills/local-docker-port-resolver
```

Restart or open a new Codex session after installation if the skill is not discovered immediately.

## Use

```text
Use $local-docker-port-resolver to add automatic host-port conflict resolution to this project's local Docker Compose stack.
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
- `agents/openai.yaml` supplies Codex UI metadata and the default prompt.

## License

MIT
