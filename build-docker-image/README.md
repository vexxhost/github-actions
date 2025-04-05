# `build-docker-image`

In order to validate that an image builds correctly, you can use the `build-docker-image` action in pull requests.

```yaml
name: build

on:
  pull_request:

jobs:
  build:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      id-token: write
    steps:
      - uses: vexxhost/github-actions/build-docker-image@main
```

In addition, if you'd like to push the image to GitHub container registry, you can use the `push` input in another workflow.

```yaml
name: publish

on:
  workflow_dispatch:
  push:
    branches:
      - main

jobs:
  image:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      id-token: write
      packages: write
      security-events: write
    steps:
      - uses: vexxhost/github-actions/build-docker-image@main
        id: build
        with:
          push: true
    outputs:
      image_name: ${{ steps.build.outputs.image-name }}
```
