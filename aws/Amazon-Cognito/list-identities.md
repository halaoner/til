# List Identities in Identity Pool

```bash
aws cognito-identity list-identities --identity-pool-id eu-east-1:8bb99048-b1dc-4a0c-b61f-12acae7e891c4 --max-results 5
```

_Output:_

```bash
{
    "IdentityPoolId": "eu-east-1:8bb04998-b1dc-4a0c-b61f-12acae7e891c4",
    "Identities": [
        {
            "IdentityId": "eu-east-1:16c0a606-f22f-4138-9f59-76734aa55409",
            "CreationDate": "2022-11-25T14:36:44.171000+01:00",
            "LastModifiedDate": "2022-11-25T14:36:44.171000+01:00"
        },
        {
            "IdentityId": "eu-east-1:2a39ad07-506b-487e-8354-0bcba2db3967",
            "CreationDate": "2022-11-25T14:34:47.251000+01:00",
            "LastModifiedDate": "2022-11-25T14:34:47.251000+01:00"
        }
    ]
}
```

# List IdentityId from Identities

```bash
aws cognito-identity list-identities --identity-pool-id eu-east-1:8bb04998-b1dc-4a0c-b61f-12acae7e891c4 --max-results 5 | jq '.Identities[0].IdentityId'
```

_Output:_

```bash
"eu-east-1:2a39ad07-506b-487e-8354-0bcba2db3967"
```