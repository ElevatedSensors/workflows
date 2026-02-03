# Elevated Sensors Shared Workflows
This repository contains reusable GitHub Action workflows for use in other Elevated Sensors repositories.

## Available Workflows
### firmware-publish.yml
- Build ESPHome firmware
- Build Hubitat Bundle
- Upload files to release (release tag name, or "nightly")
- Upload files to [docs repo](https://github.com/ElevatedSensors/docs) (build-type = "release" only)
```
name: Formal Release Example

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
      build-type: "release"
    secrets:
      DOCS_REPO_TOKEN: ${{ secrets.DOCS_REPO_TOKEN }}
```
```
name: Nightly Build Example

on:
  push:
    branches: [main]
  schedule:
    - cron: '0 7 * * *'   # run every day at 07:00 UTC
  workflow_dispatch:

jobs:
  nightly:
    permissions:
      contents: write
      pull-requests: write
    uses: ElevatedSensors/workflows/.github/workflows/publish-firmware.yml@main
    with:
      product-name: "bed-presence-mk1"
      build-type: "nightly"
    secrets:
      DOCS_REPO_TOKEN: ${{ secrets.DOCS_REPO_TOKEN }}
```
