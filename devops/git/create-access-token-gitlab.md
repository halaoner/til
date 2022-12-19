# Create Access Token For GitLab Repository

```bash
curl --request POST --header "PRIVATE-TOKEN: <personal-access-token>"--header "Content-Type:application/json"--data '{ "name":"test_token", "scopes":["api", "read_repository"], "expires_at":"2023-01-31", "access_level": 30 }'"https://gitlab.com/api/v4/projects/<project-id>/access_tokens"| jq 
```
 
Output:

```bash
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   364  100   257  100   107    497    207 --:--:-- --:--:-- --:--:--   716
{
  "id": 1634,
  "name": "test_token",
  "revoked": false,
  "created_at": "2022-11-22T15:23:20.742+01:00",
  "scopes": [
    "api",
    "read_repository"  ],
  "user_id": 1489,
  "last_used_at": null,
  "active": true,
  "expires_at": "2023-01-31",
  "access_level": 30,
  "token": "glpat-9hz7-xU2koc6xh6nUy2A"} 
```
 
# Create Group Access Token For GitLab Repository

```bash
curl --request POST --header "PRIVATE-TOKEN: <personal-access-token>"\
--header "Content-Type:application/json"\
--data '{ "name":"test_token", "scopes":["api", "read_repository"], "expires_at":"2023-01-31", "access_level": 30 }'\
"https://gitlab.com/api/v4/groups/<group-id>/access_tokens"| jq
```
 
Error Output:

```bash
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   199  100    92  100   107     66     77  0:00:01  0:00:01 --:--:--   145
{
  "message": "400 Bad request - Could not provision developer access to project access token"} 
```

The `jq` command is used to transform JSON data into a more readable format and print it to the standard output on Linux.