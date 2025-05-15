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

WIP:
compare-pypi-versions

```yaml
  check_pypi:
    needs: details
    runs-on: ubuntu-latest
    steps:
      - name: Compare Versions
        uses: ./github/actions/compare-versions
        with:
          package_name: ${{ env.PACKAGE_NAME }}
          new_version: ${{ needs.details.outputs.new_version }}
```

<!--
git tag -a v1.0.0 -m "Initial release of setup-python-poetry"
git push origin v1.0.0
-->
