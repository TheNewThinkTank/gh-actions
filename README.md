# gh-actions

Reusable GitHub workflows and Actions

## Workflows usage examples

usage of `release.yml`:

Create consuming workflow, e.g. `.github/workflows/project-release.yml`:

```yaml
name: Shared-Release-Workflow

on:
  push:
    tags:
      - "[0-9]+.[0-9]+.[0-9]+"
      - "[0-9]+.[0-9]+.[0-9]+a[0-9]+"
      - "[0-9]+.[0-9]+.[0-9]+b[0-9]+"
      - "[0-9]+.[0-9]+.[0-9]+rc[0-9]+"

jobs:
  call-release-workflow:
    uses: TheNewThinkTank/gh-actions/.github/workflows/release.yaml@v1.0.4
    with:
      PACKAGE_NAME: "package-name"
      OWNER: "github-org-or-username"
```

## Actions usage examples

setup-python-poetry:

```yaml
- name: Setup Python and Poetry
  uses: TheNewThinkTank/gh-actions/.github/actions/setup-python-poetry@v1.0.4
  with:
    python-version: ${{ env.PYTHONVERSION }}
```

setup-python-uv:

```yaml
- name: Setup Python and uv
  uses: TheNewThinkTank/gh-actions/.github/actions/setup-python-uv@v1.0.4
  with:
    python-version: '3.11'
    dependency-file: pyproject.toml  # or requirements.txt
```

compare-pypi-versions:

```yaml
- name: Compare Versions
  uses: TheNewThinkTank/gh-actions/.github/actions/compare-pypi-versions@v1.0.4
  with:
    package_name: my-package
    new_version: 1.2.3
```

<!--
git tag -a v1.0.0 -m "Initial release of setup-python-poetry"
git push origin v1.0.0
-->
