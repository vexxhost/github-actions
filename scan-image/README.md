# `scan-image`

If you'd like to schedule periodic scans of your images, you can use the `scan-image` action in a workflow.

```yaml
name: periodic

on:
  schedule:
    - cron: "0 0 * * *"

jobs:
  scan:
    runs-on: ubuntu-latest
    permissions:
      contents: read
      security-events: write
    steps:
      - uses: vexxhost/github-actions/scan-image@main
        with:
          image-ref: ghcr.io/vexxhost/ubuntu:latest
```
