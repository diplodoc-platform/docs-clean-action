# docs-clean-action GitHub action

## Inputs

- `revision` (required) - The revision or version identifier to be deleted from S3.
- `project-name` (required) - The documentation's project name, as specified in the configuration file's field with the corresponding name.
- `storage-bucket` (required) - The name of the S3 bucket where the documentation is stored.
- `storage-endpoint` (required) - The endpoint URL of the S3 service.
- `storage-access-key-id` (required) - The access key ID associated with the account that has permission to access and upload to the specified S3 bucket.
- `storage-secret-access-key` (required) - The secret access key associated with the account.
- `storage-region` (required) - The region where the specified S3 bucket is located.
- `shared-storage-bucket` (default: `false`) - Flag whether the bucket is shared across multiple projects.

## Example

```yaml
name: Remove PR revision

on:
  pull_request:
    types:
      - closed

jobs:
  remove-pr-rev:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3
      - name: Clean
        uses: diplodoc-platform/docs-clean-action@v1
        with:
          revision: "pr-${{ github.event.pull_request.number }}"
          project-name: ${{ secrets.DIPLODOC_PROJECT_NAME }}
          storage-bucket: ${{ secrets.DIPLODOC_STORAGE_BUCKET }}
          storage-endpoint: ${{ vars.DIPLODOC_STORAGE_ENDPOINT }}
          storage-access-key-id: ${{ secrets.DIPLODOC_ACCESS_KEY_ID }}
          storage-secret-access-key: ${{ secrets.DIPLODOC_SECRET_ACCESS_KEY }}
          storage-region: ${{ vars.DIPLODOC_STORAGE_REGION }}
```
