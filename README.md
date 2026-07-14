# PR Size

GitHub Action that scores PR complexity and posts a breakdown comment on every pull request.

No AI keys. No setup beyond adding the workflow. Works out of the box.

## Usage

```yaml
name: PR Size

on:
  pull_request:

jobs:
  pr-size:
    runs-on: ubuntu-latest
    permissions:
      pull-requests: write
    steps:
      - uses: iteebz/pr-size@v1
```

That's it. On every PR you get a comment like:

```
## 🟠 PR Size: L (55/100 · C+)

| Metric        | Value              | Threshold |
|---------------|--------------------|-----------|
| Lines changed | 523 (+410 / -113)  | 400       |
| Files changed | 8                  | 20        |

Exceeds line threshold (400). Large diffs are harder to review safely.
```

## Inputs

| Input | Description | Default |
|-------|-------------|---------|
| `github-token` | Token for posting comments | `${{ github.token }}` |
| `max-lines` | Line threshold before flagging large | `400` |
| `max-files` | File count threshold before flagging large | `20` |
| `fail-on-large` | Fail the check if thresholds exceeded | `false` |

## Outputs

| Output | Description |
|--------|-------------|
| `lines-changed` | Total lines added + removed |
| `files-changed` | Number of files changed |
| `size-label` | XS / S / M / L / XL / XXL |

## Size labels

| Label | Lines |
|-------|-------|
| XS | ≤ 10 |
| S  | ≤ 50 |
| M  | ≤ 150 |
| L  | ≤ 400 |
| XL | ≤ 800 |
| XXL | > 800 |

## Fail on large PRs

```yaml
- uses: iteebz/pr-size@v1
  with:
    max-lines: '300'
    max-files: '15'
    fail-on-large: 'true'
```

## License

MIT
