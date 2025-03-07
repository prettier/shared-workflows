# Shared workflows for Prettier organization

About [reuseable workflows](https://docs.github.com/en/actions/sharing-automations/reusing-workflows).

## automated-fix.yml

```yml
name: autofix.ci # needed to securely identify the workflow

on:
  pull_request:

concurrency:
  group: ${{ github.workflow }}-${{ github.ref }}
  cancel-in-progress: true

jobs:
  fix:
    name: Run automated fix
    uses: prettier/shared-workflows/.github/workflows/automated-fix.yml@main
    with:
      repository: prettier/prettier
      script: |
        yarn
        yarn fix || true
```
