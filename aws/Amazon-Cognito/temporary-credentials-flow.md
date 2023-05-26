# Generate AWS Temporary Credentials Flow

The following diagram addresses how temporary credentials are obtained for an `unauthenticated ` user when uploading a GPG Public Key into Amazon S3 by using a [pre-signed URL](https://docs.aws.amazon.com/AmazonS3/latest/userguide/using-presigned-url.html).

The following diagram describes the flow of obtaining AWS temporary credentials for an `unauthenticated ` user done by [AWS SDK for JavaScript](https://docs.aws.amazon.com/sdk-for-javascript/v3/developer-guide/welcome.html).

![obtain temporary credentials](/aws/Amazon-Cognito/diagrams/getting-temporary-credentials-flow.png)
