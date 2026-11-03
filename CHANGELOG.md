# Changelog

All notable changes to this project are documented here.

## [2.0.0] - 2026-11-03

### Changed

- Synchronized the packaged skill, Node/Compose reference, and Codex UI metadata with the global version 2.0.0 skill.
- **Breaking:** Applying the skill now standardizes full-stack startup and JavaScript dependency management on pnpm, including migration from npm, Yarn, or Bun unless the user explicitly requires another manager. Version 1.6 preserved the existing package manager.
- Added migration guidance for exact pnpm version pins, supported lockfile imports, frozen installs, dependency build-script approvals, Docker/CI alignment, and production packaging verification while preserving dependency versions where possible.
- Projects without JavaScript packages may expose the launcher through a private root package while retaining native backend tools and existing launcher implementations.
- Aligned the README and contribution checklist with the new package-manager policy and required skill validators.
- Includes the launcher changes recorded under 1.6.0, which were not previously published as a GitHub release.

## [1.6.0] - 2026-09-05

Release-status clarification (2026-11-03): these changes were committed but not tagged or published as a GitHub release. They are included in v2.0.0.

### Added

- A canonical `dev:up` full-stack launcher convention, including `pnpm dev:up` for pnpm-managed repositories and the equivalent command for other existing package managers.

### Changed

- Existing full-stack launcher names such as `local:up` are replaced without compatibility aliases, with every caller and document updated.
- Skill and Codex UI descriptions now identify the project-native launcher behavior alongside automatic port conflict resolution.

## [1.5.0] - 2026-09-01

### Added

- Explicit Gemini CLI, OpenCode, and Cline compatibility and installation guidance.
- A verification column distinguishing official platform support from live testing of this repository.

## [1.4.0] - 2026-09-01

### Added

- Explicit Cursor compatibility and installation guidance for user-level and project-level skills.

## [1.3.0] - 2026-09-01

### Added

- Repository-local `AGENTS.md` guidance that makes the generated launcher the preferred startup path for coding agents.

### Changed

- Launcher preference is project-scoped by default; global agent instructions are left unchanged unless explicitly requested.

## [1.2.0] - 2026-09-01

### Added

- Launch-focused README with badges, quick-start commands, and a before-and-after example.
- Social-preview artwork, contribution guidance, security policy, and structured issue forms.
- GitHub-discoverable `skills/<name>` package layout.

### Changed

- Enabled private vulnerability reporting for the public repository.

## [1.1.0] - 2026-09-01

### Added

- Portable Agent Skills metadata.
- Installation and compatibility guidance for Codex, Claude Code, GitHub Copilot, and other compatible clients.
- Independent Agent Skills reference validation.

## [1.0.0] - 2026-09-01

### Added

- Initial framework-neutral workflow for resolving enabled Docker Compose host-port conflicts.
- Data-driven multi-service selection, strict overrides, bounded fallback, URL synchronization, and verification guidance.
- Node.js and Docker Compose implementation reference.

[1.1.0]: https://github.com/1ntekhab/local-docker-port-resolver/releases/tag/v1.1.0
[1.0.0]: https://github.com/1ntekhab/local-docker-port-resolver/releases/tag/v1.0.0
[1.2.0]: https://github.com/1ntekhab/local-docker-port-resolver/releases/tag/v1.2.0
[1.3.0]: https://github.com/1ntekhab/local-docker-port-resolver/releases/tag/v1.3.0
[1.4.0]: https://github.com/1ntekhab/local-docker-port-resolver/releases/tag/v1.4.0
[1.5.0]: https://github.com/1ntekhab/local-docker-port-resolver/releases/tag/v1.5.0
[1.6.0]: https://github.com/1ntekhab/local-docker-port-resolver/commit/516a4311bdd52061a4f0618814c920246403e422
[2.0.0]: https://github.com/1ntekhab/local-docker-port-resolver/releases/tag/v2.0.0
