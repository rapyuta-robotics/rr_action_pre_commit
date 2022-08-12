# rapyuta-robotics/rr_action_pre_commit

A custom GitHub action to run a pre-configured verion of
[pre-commit](https://pre-commit.com). Based on the original
[pre-commit](https://github.com/pre-commit/action) action.

### Using this action

To use this action, make a file `.github/workflows/pre-commit.yml`. Here's a
template to get started:

```yaml
name: pre-commit

on:
  pull_request:
  push:
    branches: [main]

jobs:
  pre-commit:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v3
      - uses: rapyuta-robotics/rr_action_pre_commit@devel
```

This does a few things:

- clones the code
- installs python
- sets up the `pre-commit` cache

### Using this action with custom invocations

By default, this action runs all the hooks against all the files. `extra_pre_commit_args`
lets users specify a single hook id and/or options to pass to `pre-commit run`.

Here's a sample step configuration that only runs the `flake8` hook against all
the files (use the template above except for the `pre-commit` action):

```yaml
- uses: rapyuta-robotics/rr_action_pre_commit@devel
  with:
    pre_commit_extra_args: flake8 --all-files
```
