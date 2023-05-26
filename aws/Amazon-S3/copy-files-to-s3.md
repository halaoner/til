# Copy to S3 Bucket

Execute the following command when you need to copy files from your local machine to the S3 bucket:

```bash
aws s3 cp <path-to-source-file-on-your-local-machine> s3://<bucket-name>/<path-to-the-file-in-s3-bucket>
```

Example:

```bash
aws s3 cp manager_mount_efs.sh s3://gitlab-runners-shared-files/manager_mount_efs.sh
upload: ./manager_mount_efs.sh to s3://gitlab-runners-shared-files/manager_mount_efs.sh
```