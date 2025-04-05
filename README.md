# `github-actions`

This repository contains a collection of reusable GitHub actions and wworkflows
which are used within our GitHub organization.

## Usage

### `image`

This reusable workflow can help with building images in pull requests, publishing
them post merge and scanning them for vulnerabilities.

```yaml
name: build

on:
  workflow_dispatch:
  pull_request:
  push:
    branches:
      - main

permissions:
  contents: read
  id-token: write
  packages: write
  security-events: write

jobs:
  image:
    uses: vexxhost/github-actions/.github/workflows/publish-image.yml@main
    with:
      image-ref: ghcr.io/${{ github.repository_owner }}/ubuntu
      push: ${{ github.event_name == 'push' }}
```
