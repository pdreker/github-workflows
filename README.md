# github-workflows

Reusable GitHub Actions workflows for my repositories, kept in one place so action
updates land here once instead of in every repository.

| Workflow | Does | Caller permissions |
|---|---|---|
| `python-ci.yaml` | `uv sync --locked`, ruff check, ruff format check, ty, pytest; a test build of the image (`linux/amd64`, no push) when the project has a `Dockerfile`; optional extra command and SonarQube Cloud scan | `contents: read` |
| `docker-image.yaml` | multi-platform build with buildx and push; `:develop` without `version`, semver tags with it | `contents: read`, plus `packages: write` for GHCR |
| `release-please.yaml` | release PR, release and tag; outputs `release_created`, `version`, `major`, `minor`, `tag_name` | `contents: write`, `pull-requests: write` |
| `pr-title.yaml` | Conventional Commits check on the PR title (repositories squash-merge) | `pull-requests: read` |

`templates/pyproject-tools.toml` is the shared starting point for ruff, ty, pytest and
uv settings. ruff cannot load settings from another repository, so each repository
copies it; deviations get a comment saying why.

## Usage

Pin a commit SHA with the version as comment; Renovate updates both.

```yaml
# .github/workflows/ci.yaml
name: CI
on:
  pull_request:
  push:
    branches: [main]
permissions:
  contents: read
jobs:
  ci:
    uses: pdreker/github-workflows/.github/workflows/python-ci.yaml@<sha> # v1.0.0
```

```yaml
# .github/workflows/release.yaml
name: release-please
on:
  push:
    branches: [main]
permissions:
  contents: read
jobs:
  release:
    permissions:
      contents: write
      pull-requests: write
    uses: pdreker/github-workflows/.github/workflows/release-please.yaml@<sha> # v1.0.0
  image:
    needs: release
    if: ${{ needs.release.outputs.release_created == 'true' }}
    permissions:
      contents: read
      packages: write
    uses: pdreker/github-workflows/.github/workflows/docker-image.yaml@<sha> # v1.0.0
    with:
      image: ghcr.io/owner/name
      version: ${{ needs.release.outputs.version }}
```

For another registry, pass `registry`, `registry-username` and the secret
`registry-password`. Secrets are always passed by name, never with `secrets: inherit`:
this repository is public and its callers include private repositories.

release-please opens its PR with `GITHUB_TOKEN`; GitHub holds the checks on it until
you approve them with "Approve workflows to run" on the PR.

Required status checks are named `<caller job> / <called job>`, e.g.
`ci / Lint, type-check, test`.

## Development

`test.yaml` runs actionlint and zizmor (`uv run actionlint`,
`uv run zizmor .github/workflows`) and calls `python-ci.yaml` and `docker-image.yaml`
against `tests/fixture`, so a change is exercised before any caller sees it. The tool
tables in `tests/fixture/pyproject.toml` copy the template; keep them in step.

Releases come from release-please (Conventional Commits on the PR title).
