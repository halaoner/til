# AWS Systems Manager Parameter Store

Put `secure string` parameter by using environment variable.

```bash
aws ssm put-parameter \
    --name "GPG-PublicKey" \
    --value $PUBLICKEY \
    --type SecureString \
    --tags "Key=GPG,Value=PublicKey" \
    --region "eu-central-1"
```