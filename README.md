# workflows

This repository contains template for Github Actions

### build-container

Usage:

```
...
jobs:
  build_and_push:
    uses: BloopAI/workflows/.github/workflows/build-container.yml@main
    with:
      repository: demo-application
      tag: build-${{ github.sha }}
    secrets:
      awsRegion: eu-west-1
      awsAccountID: "<accound-id>"
      slackBuildWebhook: ${{ secrets.SLACK_BUILD_WEBHOOK }}
```

### Validate helm chart

Usage:

```
...
jobs:
  validate_helm:
    uses: BloopAI/reusable-workflows/.github/workflows/validate-helm-chart.yml@main
    with:
      path: helm/demo-application
    secrets:
      slackBuildWebhook: ${{ secrets.SLACK_BUILD_WEBHOOK }}
```

### Release tag

```
name: Release tag

on:
  push:
    branches:
      - 'release/v*.*.*'

jobs:
  release_tag:
    uses: BloopAI/workflows/.github/workflows/release-tag.yml@release-branch-worfklow
    with:
      gitUsername: devops
      gitEmail: <email>
    secrets:
      slackBuildWebhook: ${{ secrets.SLACK_BUILD_WEBHOOK }}
      pat: ${{ secrets.PAT }}
```