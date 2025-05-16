# gh-actions

Reusable GitHub Actions

## Usage examples

setup-python-poetry:

```yaml
- name: Setup Python and Poetry
  uses: TheNewThinkTank/gh-actions/.github/actions/setup-python-poetry@v1.0.1
  with:
    python-version: ${{ env.PYTHONVERSION }}
```

setup-python-uv:

```yaml
- name: Setup Python and uv
  uses: TheNewThinkTank/gh-actions/.github/actions/setup-python-uv@v1.0.1
  with:
    python-version: '3.11'
    dependency-file: pyproject.toml  # or requirements.txt
```

compare-pypi-versions:

```yaml
- name: Compare Versions
  uses: TheNewThinkTank/gh-actions/.github/actions/compare-pypi-versions@v1.0.2
  with:
    package_name: my-package
    new_version: 1.2.3
```

<!--
git tag -a v1.0.0 -m "Initial release of setup-python-poetry"
git push origin v1.0.0
-->
