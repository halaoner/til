# Download Files from S3 Bucket

## Cannot execute `aws` CLI command

When got this error:

```bash
[ec2-user@ip-10-35-0-68 ~]$ sudo aws s3api get-object --bucket gitlab-runners-shared-files --key config.toml /etc/gitlab-runner/config.toml

An error occurred (SignatureDoesNotMatch) when calling the GetObject operation: The request signature we calculated does not match the signature you provided. Check your key and signing method.
```

Check your credentials in `~.aws/` folder. Re-exeute `aws configure` command if necessary.