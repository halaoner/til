# HashiCorp Vault in Docker container

Run the following command to access `S3_ACCEESS_KEY` and `S3_SECRET_KEY`:

```bash
curl --header "X-Vault-Token: <access-token>" http://127.0.0.1:8200/v1/secret/data/aws/ti8m-test-user | jq '.data.data'
```

_Output:_

```bash
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   399  100   399    0     0  12085      0 --:--:-- --:--:-- --:--:-- 23470
{
  "S3_ACCESS_KEY": "here-is-s3-access-key",
  "S3_SECRET_KEY": "here-is-s3-secret-key"
}
```
