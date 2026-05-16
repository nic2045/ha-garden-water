# ha-garden-water — Development Guide

## Commit conventions (Conventional Commits)

All commits must follow [Conventional Commits](https://www.conventionalcommits.org/):

| Prefix | Semver effect | When to use |
|--------|---------------|-------------|
| `feat: ...` | minor bump (0.9.x → 0.10.0) | New user-facing blueprint feature |
| `fix: ...` | patch bump (0.9.7 → 0.9.8) | Bug fix or behaviour correction |
| `chore: ...` | no bump | Tooling, CI, dependencies |
| `docs: ...` | no bump | README, CHANGELOG, comments |
| `refactor: ...` | no bump | Code restructure, no behaviour change |
| `feat!: ...` / `BREAKING CHANGE` | major bump | Removes or renames existing inputs |

## Release workflow

Releases are fully automated via [release-please](https://github.com/googleapis/release-please):

1. Merge `feat:` / `fix:` commits to `main`
2. release-please opens a **Release PR** automatically (updates `CHANGELOG.md` + `version.txt`)
3. Review and merge the Release PR
4. GitHub Release + tag are created; the blueprint version in `garden_irrigation.yaml` is stamped automatically

Do **not** manually edit `version.txt` or bump the version string in `garden_irrigation.yaml` — the workflow handles that.

## Branch strategy

- `main` — stable, always importable from the My HA badge
- Feature branches — one branch per feature, PR into main
- Branch naming: `feat/<topic>` or use Claude Code's generated names

## Key files

| File | Purpose |
|------|---------|
| `garden_irrigation.yaml` | The blueprint — single source of truth |
| `version.txt` | Current version, managed by release-please |
| `CHANGELOG.md` | Auto-updated by release-please on each release |
| `.release-please-manifest.json` | Last released version (do not edit manually) |
| `release-please-config.json` | release-please configuration |
| `.github/workflows/validate.yaml` | CI: YAML syntax check on every push/PR |
| `.github/workflows/release-please.yaml` | CI: automated release on push to main |

## Blueprint versioning

The version string inside `garden_irrigation.yaml` is managed automatically.
Format: `**Version: vX.Y.Z**` — the CI stamps this after each release.
