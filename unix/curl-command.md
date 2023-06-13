# curl command

Get `HTTP` code from the `curl` command:

```bash
curl \
    -I \
    -w "HTTP code: %{http_code}" \
    -s \
    -X GET \
    --header "PRIVATE-TOKEN: $ACCESS_TOKEN" "https://gitlab.com/api/v4/projects" > httpCode.txt
```            