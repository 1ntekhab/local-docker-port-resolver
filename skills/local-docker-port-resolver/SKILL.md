---
name: local-docker-port-resolver
description: Add or repair automatic host-port selection for enabled services in local Docker Compose stacks. Use when development or local simulation launchers must avoid conflicts across applications, proxies, mail UIs, dashboards, and other published services while synchronizing public URLs. Keep actual production endpoints explicit.
license: MIT
metadata:
  author: 1ntekhab
  version: "1.4.0"
  compatibility: Agent Skills-compatible coding agents with repository file and shell access; Docker Compose is required for rendered configuration and live verification.
---

# Local Docker Port Resolver

Add predictable local Docker Compose port fallback without changing internal service ports or actual production addressing.

## Inspect before changing anything

- Find every supported local mode and start command, package-manager script, Compose file and overlay, profile, environment example, and run document.
- Render or inspect each selected mode to identify every enabled host-published port. Record a target name, Compose service and fixed container port, host-port environment variable, preferred default, bind address, displayed URL, and whether the service is optional.
- Inspect profiles and overlays before deciding that a target is active. Never enable Grafana, Mailpit, a debugger, or another optional service merely so its port can be resolved.
- Search for every consumer of the primary or auxiliary public URLs: backend base URLs, CSRF/CORS/WebSocket origins, OAuth callbacks, frontend API configuration, E2E defaults, health checks, MFA/WebAuthn relying-party origins, proxy redirects, mail links, dashboards, and generated links.
- Preserve unrelated working-tree changes. Do not read or print unrelated secrets from local environment files or rendered Compose output.

## Choose the launcher integration

- Prefer the language/runtime already required by the repository and wire the launcher into its existing local start command.
- Keep direct lower-level startup commands available for advanced use unless the user requests their removal.
- Avoid a new dependency when the existing runtime provides socket probing, process spawning, and environment parsing.
- For a Node.js plus Docker Compose implementation, read [the verified Node/Compose pattern](references/node-compose-pattern.md).
- Make the supported launcher the documented project startup path. When the repository uses `AGENTS.md`, add or update a repository-local instruction that tells coding agents to prefer the launcher over direct Compose startup while preserving existing instructions.
- Keep this preference project-scoped. Do not modify a user's global Codex, Claude, Copilot, or other agent instructions unless the user explicitly requests a global policy.

## Preserve the port contract

- Use a data-driven target registry rather than one branch of logic per service. Resolve only targets present in the selected mode/profile.
- Resolve each preferred host port in this order: explicit named command option, process environment, selected mode's environment file, then repository default. Preserve an existing numeric `--port` form as the primary application shorthand when compatibility requires it.
- Treat every explicit command-line port as strict. Reject duplicate, unknown, inactive-target, malformed, or unavailable overrides clearly instead of silently choosing another.
- For automatic fallback, scan a documented bounded range and stop with a target-specific error when it is exhausted.
- Check loopback and wildcard binding. A wildcard-only probe can incorrectly report a loopback-bound Docker port as free on Windows.
- Reserve every port selected during the run so two targets cannot receive the same host port, even if operating-system probes report the not-yet-started choices as free.
- Query current mappings by Compose service and container port. If the same project is already running on a fallback port and the preferred port is occupied, reuse that target's current mapping instead of drifting.
- Change only the published host port. Preserve reverse-proxy and application container ports.
- Derive all primary and auxiliary URLs after the full target set is selected. Pass them to every backend security, proxy, frontend, testing, and operational consumer in the startup environment. Replace stale local origins while preserving non-local configured origins.
- Leave relative frontend API paths unchanged; the browser inherits the selected origin. Adapt absolute frontend URLs, callbacks, or test runners explicitly when the project uses them.
- Do not rewrite a developer's environment file merely to communicate a runtime choice unless the user explicitly requests persistence.
- When follow-up commands run separately, persist only the resolved host ports and derived public URLs in an ignored, mode-specific state file. Keep it separate from generated secrets, serialize a fixed allowlist safely, and load both files in the documented order.
- Keep actual production and staging URLs explicit. A local production simulation may use fallback only when the project explicitly supports that mode; never turn a real production launch into a dynamic one.

## Verify the result

- Unit-test multi-target precedence, numeric and named parsing, strict per-target failures, bounded exhaustion, duplicate avoidance, inactive optional services, current-project reuse, synchronized URLs, and safe state serialization.
- Validate each mode's rendered mappings and consumers while outputting only relevant, non-secret fields.
- Run live conflict tests with preferred ports genuinely occupied. Verify the primary health/redirect paths and every enabled auxiliary endpoint through the reported ports.
- Start each mode a second time and confirm it reuses every current project mapping.
- Confirm normal environment files, generated secret files, and unrelated tracked files are unchanged; only an explicitly designed resolved-state file may change.
- Run the repository's normal controls and document automatic startup, named strict overrides, optional-profile behavior, printed URLs, state loading, and the difference between host and container ports.
