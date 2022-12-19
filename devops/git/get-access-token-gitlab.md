# Get Access Token per GitLab repository

```bash
curl --header "PRIVATE-TOKEN: <personal-access-token>""https://gitlab.com/api/v4/projects/<project-id>/access_tokens"| jq 
```
 
Output:

```bash 
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   364  100   257  100   107    506    210 --:--:-- --:--:-- --:--:--   725
{
  "id": 1631,
  "name": "test_token",
  "revoked": false,
  "created_at": "2022-11-22T15:06:35.027+01:00",
  "scopes": [
    "api",
    "read_repository"  ],
  "user_id": 1484,
  "last_used_at": null,
  "active": true,
  "expires_at": "2023-01-31",
  "access_level": 30,
  "token": "glpat-3224wdsadasdas"} 
```

The `jq` command is used to transform JSON data into a more readable format and print it to the standard output on Linux.