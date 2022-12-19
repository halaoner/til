# Get Statistics From GitLab Project

Get statistical data from GitLab project with pipe into `jq` command.

```bash
curl-XGET --header"PRIVATE-TOKEN:AAABBBCCC"https://gitlab.com/api/v4/projects/4158/statistics | jq
```

The `jq` command is used to transform JSON data into a more readable format and print it to the standard output on Linux.