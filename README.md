# codepipeline-webhook-action

- This action sends a POST request to `codepipeline_webhook_url` with `codepipeline_webhook_secret` in `x-api-key` header
- This is currently used to trigger AWS Codepipeline(indirectly via a [lambda](https://github.com/medlypharmacy/trigger-codepipeline-deployment)) for GitHub repository that uses this action

## Usage

You can add the below step in your Actions workflow after uploading the artifacts to S3 with the [s3-artifacts-action](https://github.com/medlypharmacy/s3-artifacts-action)

```yaml
- name: Deploy to dev env
  uses: medlypharmacy/codepipeline-webhook-action@master
  if: github.ref == 'refs/heads/master'
  with:
  deployment_environment: 'dev'
  codepipeline_webhook_url: ${{ secrets.CODEPIPELINE_WEBHOOK_URL }}
  codepipeline_webhook_secret: ${{ secrets.CODEPIPELINE_WEBHOOK_SECRET }}
```
