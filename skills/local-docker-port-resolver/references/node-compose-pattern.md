# Verified Node.js and Docker Compose Pattern

Use this pattern when a repository already requires Node.js and starts its local stack with Docker Compose. Adapt names and consumers to the project; do not assume Nginx, Django, or Next.js unless inspection confirms them.

## Launcher sequence

For pnpm repositories, register the resolver-backed launcher as the `dev:up` package script and document `pnpm dev:up` as the only full-stack development command. Replace established names such as `local:up`, update all callers, and remove the old scripts without compatibility aliases. With other package managers, retain that manager and use its equivalent `dev:up` script.

1. Select a named local mode and its Compose files, profiles, environment files, and project name.
2. Ask Compose for the services active in that selection, then filter a data-driven port-target registry to those services. Do not activate optional profiles during discovery.
3. Parse strict repeatable named overrides such as `--port app=8090` and `--port mailpit=8026`. If the repository already exposes numeric `--port 8090`, retain it as the primary application shorthand.
4. For each active target, read its preferred port from the matching explicit override, process environment, selected mode environment file, then documented default.
5. Query the running project's mapping with `docker compose port <service> <container-port>` so repeated starts can reuse a prior fallback.
6. Resolve targets in stable registry order. Probe each candidate by briefly binding both `127.0.0.1` and `0.0.0.0`, and reserve every selection in memory to prevent cross-target duplicates.
7. If an automatic preferred port is occupied, reuse that target's current project mapping or scan the bounded range. If an explicit choice is occupied, fail for that target without fallback.
8. After every target is selected, derive the primary origin, trusted origins, redirect destinations, test base URL, and auxiliary URLs from the shared result.
9. Build a child-process environment containing published ports and synchronized derived values. For multi-command modes, atomically write a secret-free ignored state file from a fixed key allowlist.
10. Validate configuration, spawn `docker compose up --build -d` with inherited output, and propagate any nonzero result.
11. Run `docker compose ps --all` and print the final application, readiness, and enabled auxiliary URLs.

Use built-in Node modules such as `node:net`, `node:child_process`, `node:fs`, and `node:util` when the supported Node version provides the required APIs.

## Target registry shape

Each local mode should provide enough metadata for generic selection and display:

| Field | Purpose |
|---|---|
| `name` | Stable CLI and diagnostic identifier such as `app`, `mailpit`, or `grafana` |
| `service` | Compose service whose host mapping is inspected |
| `containerPort` | Fixed internal port; never rewritten by fallback |
| `environmentVariable` | Published host-port input passed to Compose |
| `defaultPort` | Preferred local host port |
| `bindAddress` | Intended published interface, commonly loopback for auxiliary tools |
| `displayUrl` | URL builder used only after resolution |
| `optional` | Whether selection depends on a profile or overlay |

Mode metadata should also define Compose arguments, its environment-file precedence, the primary target, and any ignored resolved-state file. Derive consumers in a mode-specific function from the generic resolution map.

## Adaptation checklist

- All enabled public and auxiliary service/container ports.
- Every preferred published-port variable and default.
- Profile and overlay activation rules.
- Backend base URL plus CSRF, CORS, WebSocket, callback, and allowed-origin settings.
- Proxy redirects, MFA/WebAuthn verifier origins, health URLs, and E2E configuration.
- Frontend relative or absolute API configuration.
- Mail viewer, metrics dashboard, debugger, storage UI, and other auxiliary links.
- Canonical `dev:up` package-manager command and argument-forwarding syntax; verify that replaced launcher names have no remaining callers.
- Follow-up commands that need the resolved-state file.
- Unit-test location and normal repository test entry point.

For an Nginx, Django, and Next.js stack, a common primary mapping is:

| Concern | Typical value |
|---|---|
| Published edge port | `NGINX_PORT` |
| Fixed Nginx container port | `80` |
| Django public origin | `APP_BASE_URL` |
| Django trusted origins | `DJANGO_CSRF_TRUSTED_ORIGINS` |
| Next.js browser API path | Relative path such as `/api/v1` |

## Failure modes to prevent

- Docker's random published port does not automatically update backends, callbacks, tests, or absolute frontend URLs.
- Resolving targets independently without a reservation set can assign the same not-yet-bound port twice.
- Treating every registry target as active can unexpectedly enable optional monitoring or debugging services.
- Persisting an entire child-process environment can leak generated secrets; serialize only approved ports and public URLs.
- `docker compose config --quiet` validates configuration shape but cannot prove that a host port is available.
- A wildcard-only socket probe can miss a loopback-specific listener on Windows.
- `docker compose ps` can hide stopped or never-started containers; use `--all` for diagnostics.
- Shells may continue after a failed Compose command, so the launcher must propagate the exit status.
- A probe-and-start race remains possible; if Compose loses that race, fail clearly and let the next invocation resolve again rather than looping without a bound.
