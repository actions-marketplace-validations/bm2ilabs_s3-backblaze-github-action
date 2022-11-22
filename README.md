# s3-upload-github-action
Upload github action for sending files to s3 like Backblaze


## Usage

This is a super straightforward action that uses the aws cli tool to copy a particular file to an s3 bucket. The file can come from your code directly or generated by an earlier part of your github actions flow. Check out the example below to get started.

Please note that each env var is required. It is recommended to put your AWS credentials in as repository secrets, as well as your bucket name.

```yaml
# inside .github/workflows/your-action.yml
name: Add File to Bucket
on: push

jobs:
  deploy:
    runs-on: ubuntu-latest
    
    steps:
   - uses: actions/checkout@master
   
   - name: S3 File Upload (BackBlaze)
     uses: bm2ilabs/s3-backblaze-github-action@v1
     with:
       args: --acl public-read
     env:
      FILE: lambda.zip
      S3_REGION: 'us-east-1'
      S3_BUCKET: ${{ secrets.S3_BUCKET }}
      S3_ENDPOINT_URL: 'https://s3.us-west-002.backblazeb2.com'
      S3_ACCESS_KEY_ID: ${{ secrets.S3_ACCESS_KEY_ID }}
      S3_SECRET_ACCESS_KEY: ${{ secrets.S3_SECRET_ACCESS_KEY }}
```
