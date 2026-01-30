# Elevated Sensors Shared Workflows
This repository contains reusable GitHub Action workflows for use in other Elevated Sensors repositories.

## Available Workflows
### firmware-publish.yml
Build ESPHome firmware, push files to release, push files to [docs repo](https://github.com/ElevatedSensors/docs).
```
name: Release

on:
  release:
    types: [released]

jobs:
  publish:
    permissions:
      contents: write
      pull-requests: write
    uses: ElevatedSensors/workflows/.github/workflows/publish-firmware.yml@main
    with:
      product-name: "bed-presence-mk1"
    secrets:
      DOCS_REPO_TOKEN: ${{ secrets.DOCS_REPO_TOKEN }}
```

### firmware-nightly.yml
Build ESPHome firmware, push files to persistent `nightly` release.
```
name: Nightly

on:
  push:
    branches: [main]
  schedule:
    - cron: '0 0 * * *'   # run every day at 00:00
  workflow_dispatch:

jobs:
  nightly:
    permissions:
      contents: write
    uses: ElevatedSensors/workflows/.github/workflows/firmware-nightly.yml@main
    with:
      product-name: "bed-presence-mk1"
```
