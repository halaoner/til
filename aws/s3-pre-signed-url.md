# Amazon S3 pre-signed URL

## GET Method

A `pre-signed URL` expires in 24 h - works only for HTTP `GET method` when generating it by the following CLI command:

```bash
aws s3 presign s3://gpg-statistics-test-bucket/public-key/  --expires-in 86400
```

_Output:_

```bash
https://gpg-statistics-test-bucket.s3.eu-central-1.amazonaws.com/public-key/?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIARAGDLGUCMVEXNKU4%2F20221115%2Feu-central-1%2Fs3%2Faws4_request&X-Amz-Date=20221115T103835Z&X-Amz-Expires=86400&X-Amz-SignedHeaders=host&X-Amz-Signature=9702c23f2f97f0d0c326ac27656e00f8991bf17115e7c0250bdcddd73ace1c51
```

## PUT Method

Generate the-signed URL by using [AWS SDK](https://docs.aws.amazon.com/AmazonS3/latest/userguide/PresignedUrlUploadObject.html) for HTTP PUT method.