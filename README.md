# gh-actions

Reusable GitHub workflows and Actions

## Workflows usage examples

### Main branch protection

The [branch protection workflow](.github/workflows/branch-protection.yml) configures
`main` in the calling repository. It requires at least one approving review,
dismisses stale approvals, requires approval of the most recent reviewable push,
and enforces protection for administrators. Existing status checks, push
restrictions, higher approval counts, code-owner requirements, and other branch
protection settings are preserved. No status checks are added automatically.

1. Create a fine-grained personal access token with access to each target repository
  and **Administration: Read and write** permission. The token owner must have
  repository administration access. The default `GITHUB_TOKEN` cannot manage
  branch protection.
2. Store the token as a repository or organization Actions secret named
  `SHARED_WORKFLOW_HOUSEKEEPING`, making it available to each target repository.
3. After publishing this reusable workflow, add the following caller workflow to
  `.github/workflows/branch-protection.yml` on `main` in each target repository:

```yaml
name: Configure Main Branch Protection

on:
  workflow_dispatch:

permissions: {}

jobs:
  branch-protection:
   uses: TheNewThinkTank/gh-actions/.github/workflows/branch-protection.yml@main
   secrets:
    SHARED_WORKFLOW_HOUSEKEEPING: ${{ secrets.SHARED_WORKFLOW_HOUSEKEEPING }}
```

Run **Configure Main Branch Protection** from the target repository's **Actions**
tab. Replace `@main` with a published tag or commit SHA for a pinned version. The
target repository must have a `main` branch and a GitHub plan that supports branch
protection for its visibility. Cross-repository callers also need access to this
repository's reusable workflows; configure Actions access if this repository is
private or internal.

The reusable workflow also supports **Run workflow** directly in this repository
(or when copied into another repository); it always protects the repository where
the run was triggered. Rerunning it reapplies the policy without removing existing
status checks or push restrictions.

### Release

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

permissions:
  id-token: write
  contents: write

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
