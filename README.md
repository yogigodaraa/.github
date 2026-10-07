# yogigodaraa/.github

Shared defaults for every repository under [@yogigodaraa](https://github.com/yogigodaraa).

GitHub automatically uses the community-health files in this repo for any of my
repos that don't have their own copy. The reusable CI workflows are called from each
repo's own `.github/workflows/ci.yml`.

## What's in here

| Path | What it does |
| --- | --- |
| `CONTRIBUTING.md` | How to propose a change (branch → PR → CI → squash merge) |
| `SECURITY.md` | How to report a vulnerability privately |
| `CODE_OF_CONDUCT.md` | Expected behaviour in issues and PRs |
| `.github/ISSUE_TEMPLATE/` | Bug report, feature request, learning task |
| `.github/pull_request_template.md` | "What does this change do? What could break? What did I learn?" |
| `.github/workflows/node-ci.yml` | Reusable CI for Node / TypeScript projects |
| `.github/workflows/python-ci.yml` | Reusable CI for Python projects |

## Using the reusable workflows

Node / TypeScript (detects npm, pnpm or yarn from the lockfile, then runs the
`lint`, `typecheck`, `test` and `build` scripts **only if they exist** in `package.json`):

```yaml
# .github/workflows/ci.yml
name: CI
on:
  pull_request:
  push:
    branches: [main]
concurrency:
  group: ci-${{ github.ref }}
  cancel-in-progress: true
permissions:
  contents: read
jobs:
  web:
    uses: yogigodaraa/.github/.github/workflows/node-ci.yml@main
    with:
      working-directory: .
```

Python (uses `uv` if there is a `uv.lock`, otherwise pip with `requirements*.txt` /
`pyproject.toml`; then `ruff check` and `pytest`):

```yaml
jobs:
  backend:
    uses: yogigodaraa/.github/.github/workflows/python-ci.yml@main
    with:
      working-directory: backend
      python-version: "3.12"
```

Useful Python inputs: `requirements` (which requirements files to install, e.g.
`requirements-optimized.txt`), `test-command`, `test-env` and `ruff-version` (pinned by default).
Ruff uses the repo's own `ruff.toml` / `[tool.ruff]` config. Newer ruff releases enable more rules
by default, so each repo should declare its rule set explicitly.

The status check that branch protection sees is named `<caller job> / test`,
e.g. `web / test` or `backend / test`. Keep the caller job ids stable.

See each workflow file for the full list of inputs.
