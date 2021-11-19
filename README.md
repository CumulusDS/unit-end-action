[![Create Release][release-badge]][release-url]
[![Import Labels][import-labels-badge]][import-labels-url]
[![Sync Labels][sync-labels-badge]][sync-labels-url]
[![PR AutoLabeler][autolabeler-badge]][autolabeler-url]
[![Assigner][assigner-badge]][assigner-url]

Description

### Inputs
#### `text`
Text for slack message
required: false
default: "${{ github.repository }} Unit Test"

#### `status`
Job Status
required: false
default: "${{ job.status }}"

#### `author_name`
Message author name for slack message
required: false
default: "${{ github.repository }} ${{ github.workflow }}"

#### `slack_webhook_url`
Slack webhook url

#### `uploadArtifactName`
Name of output artifact
default: upload-artifacts

#### `artifactPath`
The path to upload as an artifact
default: var

#### `githubEventAction`
GitHub event action context
default: "${{ github.event.action }}"

#### `githubEventName`
GitHub event name context
default: "${{ github.event_name }}"

### Example usage
```yaml
      - name: Upload, determine trigger, set feature stage, set matrix
        id: end
        uses: Cumulusds/unit-end-action@v1
        if: always()
```

The results can be later referenced again for use in a separate step if desired using the `results` output from the step.
In order to reference the `result` output, you must assign and `id` to the step for future referencing.

```yaml
      - name: reprint results
        run: |
          echo "${{ steps.action.end.stage }}"
          echo "${{ steps.action.end.matrix }}"
```
Or as outputs from a job:
```yaml
jobs:
  unit:
    outputs:
      matrix: ${{ steps.end.outputs.matrix }}
      stage: ${{ steps.end.outputs.stage }}
```


[release-badge]: https://github.com/CumulusDS/unit-end-action/actions/workflows/release.yml/badge.svg
[release-url]: https://github.com/CumulusDS/unit-end-action/actions/workflows/release.yml
[import-labels-badge]: https://github.com/CumulusDS/unit-end-action/actions/workflows/labels_import.yml/badge.svg
[import-labels-url]: https://github.com/CumulusDS/unit-end-action/actions/workflows/labels_import.yml
[sync-labels-badge]: https://github.com/CumulusDS/unit-end-action/actions/workflows/labels_sync.yml/badge.svg
[sync-labels-url]: https://github.com/CumulusDS/unit-end-action/actions/workflows/labels_sync.yml
[autolabeler-badge]: https://github.com/CumulusDS/unit-end-action/actions/workflows/autolabeler.yml/badge.svg
[autolabeler-url]: https://github.com/CumulusDS/unit-end-action/actions/workflows/autolabeler.yml
[assigner-badge]: https://github.com/CumulusDS/unit-end-action/actions/workflows/assign.yml/badge.svg
[assigner-url]: https://github.com/CumulusDS/unit-end-action/actions/workflows/assign.yml
