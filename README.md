# yampl-action

This action runs [yampl](https://github.com/clevyr/yampl) to template values in a yaml file.

See the [yampl](https://github.com/clevyr/yampl#readme) readme for more details on yampl templating capabilities.

# Usage

## Inputs

- `file` - Path to the file that should be patched.
- `values` - List of values to replace in the provided file.
- `commit_message` - If set, this action will invoke [stefanzweifel/git-auto-commit-action](https://github.com/stefanzweifel/git-auto-commit-action) with the given commit message.
- `yampl_version` - Yampl version to install

## Outputs

None

## Example Workflow

Here is an example that fetches a separate deployment repo and patches its configuration.

```yaml
name: Patch Configuration

on: push

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout
        uses: actions/checkout@v2

      - id: short-sha
        uses: benjlevesque/short-sha@v1.2

      - name: Bump version
        uses: clevyr/yampl-action@v1
        with:
          file: deployment.yaml
          values: |
            tag=${{ github.sha }}
          commit_message: ":arrow_up: Bump deployment to ${{ steps.short-sha.outputs.sha }}"
```
