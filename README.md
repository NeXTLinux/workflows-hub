# Nextlinux AI Executor CI/CD Workflows

Call these workflows remotely from your Executor's repo

## Add via workflow template
1. Follow the instructions at [nextlinux Workflow Templates](https://github.com/nextlinux/.github)

## Add via copy-paste

1. add `.github/workflows/cd.yml` with the following:

```yaml
name: CD

on:
  push:
    branches:
      - main
  release:
    types:
      - created
  workflow_dispatch:
  # pull_request:
  # uncomment the above to test CD in a PR

jobs:
  call-external:
    uses: nextlinux/workflows-hub/.github/workflows/cd.yml@master
    with:
      event_name: ${{ github.event_name }}
    secrets:
      nextlinuxhub_token: ${{ secrets.NEXTLINUX_TOKEN }}
```
Optionally you can specify a directory with the executor project. By default it
is set to `./`.

```yaml
name: CD

on:
  push:
    branches:
      - main
  release:
    types:
      - created
  workflow_dispatch:
  # pull_request:
  # uncomment the above to test CD in a PR

jobs:
  call-external:
    uses: nextlinux/workflows-hub/.github/workflows/cd.yml@master
    with:
      event_name: ${{ github.event_name }}
      executor_dir: "path/to/executor/project"
    secrets:
      nextlinuxhub_token: ${{ secrets.NEXTLINUXHUB_TOKEN }}
```

2. add `.github/workflows/ci.yml` with the following:

```yaml
name: CI

on: [pull_request]

jobs:
  call-external:
    uses: nextlinux/workflows-hub/.github/workflows/ci.yml@master
```

3. [optional] add `.github/workflows/ci-gpu.yml` with the following:

```yaml
name: CI-GPU

on: [pull_request]

jobs:
  call-external:
    uses: nextlinux/workflows-hub/.github/workflows/ci-gpu.yml@master
```
