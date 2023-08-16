# s3 Sync Command

S3 sync compares the size of the file and the last modified timestamp to see if a file needs to be synced.

> 💡 `aws s3 sync` looks at the destination before copying files over and only copies over files that are new and updated

```bash
aws s3 sync . s3://s3-bucket-name --exclude "*" --exclude "pre_build_script.sh" --include "config.toml" --include "gitlab-runners_userdata.sh" --size-only
```

`--exclude` (string) Exclude all files or objects from the command that matches the specified pattern.

`--include` (string) Don't exclude files or objects in the command that match the specified pattern.

`--size-only` (boolean) Makes the size of each key the only criteria used to decide whether to sync from source to destination.

## References

- [aws s3 cp vs aws s3 sync behavior and cost](https://stackoverflow.com/questions/64728076/aws-s3-cp-vs-aws-s3-sync-behavior-and-cost)
- [aws s3 sync](https://docs.aws.amazon.com/cli/latest/reference/s3/sync.html)
- [aws s3 sync command based on file size only?](https://stackoverflow.com/questions/42786179/aws-s3-sync-command-based-on-file-size-only)
- [AWS S3 Sync Example](https://levelup.gitconnected.com/aws-s3-sync-example-fc53be7e646b)
