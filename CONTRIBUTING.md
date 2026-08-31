# Contributing

Thank you for helping Local Docker Port Resolver support more local development stacks.

## Good contributions

- Reproducible fixes for Docker Compose port-discovery or URL-propagation behavior.
- Framework-specific examples that preserve the framework-neutral workflow.
- Coverage for optional Compose profiles and auxiliary services.
- Documentation improvements backed by tested commands.

## Before opening a pull request

1. Open an issue for substantial behavior changes so the scope can be discussed.
2. Keep automatic fallback limited to local development and explicitly supported local simulations.
3. Keep internal container ports fixed unless the application itself requires an internal change.
4. Never make real production endpoints dynamic.
5. Do not add secrets, generated credentials, local environment files, or project-specific private data.
6. Validate the skill with an Agent Skills-compatible validator.
7. Test instructions against a representative Compose project and describe the evidence in the pull request.

## Pull request checklist

- [ ] `skills/local-docker-port-resolver/SKILL.md` still has valid frontmatter and matches its directory name.
- [ ] New published ports and every consumer of their public URLs are covered.
- [ ] Explicit overrides fail clearly when unavailable.
- [ ] Optional services remain opt-in.
- [ ] Documentation and examples match the behavior.
- [ ] No secrets or unrelated generated files are included.

By contributing, you agree that your contribution is licensed under the repository's MIT License.
