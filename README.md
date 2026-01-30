# Elevated Sensors Shared Workflows
This repository contains reusable GitHub Action workflows for use in other Elevated Sensors repositories.

## Available Workflows
### publish-firmware.yml
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
