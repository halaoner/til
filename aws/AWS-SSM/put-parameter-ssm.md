# AWS Systems Manager Parameter Store

Put `secure string` parameter by using environment variable.

```bash
aws ssm put-parameter \
    --name "Key" \
    --value $KEYID \
    --type SecureString \
    --tags "Key=test,Value=testing" \
    --region "eu-east-1"
```