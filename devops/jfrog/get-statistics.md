# Get Statistics From JFrog Artifactory

How to get number of downloads from Artifactory, e.g., for statistical purposes - how many times a Docker image has been downloaded.

```bash
 time curl -X GET -u username:access-token https://url:443/artifactory/api/storage/docker-image/pre-commit/1.1/list.manifest.json\?stats | jq
```

Output:

```bash
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   251    0   251    0     0    108      0 --:--:--  0:00:02 --:--:--   108
{
  "uri": "https://url:443/artifactory/docker-image/pre-commit/1.1/list.manifest.json",
  "downloadCount": 4,
  "lastDownloaded": 1671043670843,
  "lastDownloadedBy": "john",
  "remoteDownloadCount": 0,
  "remoteLastDownloaded": 0
}
curl -X GET -u    0.01s user 0.01s system 0% cpu 2.330 total
jq  0.01s user 0.00s system 0% cpu 2.330 total
```

The `jq` command is used to transform JSON data into a more readable format and print it to the standard output on Linux.