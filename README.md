# docs-clean-action GitHub action

## Inputs

- `revision` (required) - The revision or version identifier to be deleted from S3.
- `s3-bucket` (required) - The name of the S3 bucket where the documentation is stored.
- `s3-endpoint` (required) - The endpoint URL of the S3 service.
- `s3-access-key-id` (required) - The access key ID associated with the account that has permission to access and upload to the specified S3 bucket.
- `s3-secret-access-key` (required) - The secret access key associated with the account.
- `s3-region` (required) - The region where the specified S3 bucket is located.

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
          s3-bucket: ${{ secrets.DOCS_AWS_BUCKET }}
          s3-endpoint: ${{ vars.DOCS_AWS_ENDPOINT }}
          s3-access-key-id: ${{ secrets.DOCS_AWS_KEY_ID }}
          s3-secret-access-key: ${{ secrets.DOCS_AWS_SECRET_ACCESS_KEY }}
          s3-region: ${{ vars.DOCS_AWS_REGION }}
```