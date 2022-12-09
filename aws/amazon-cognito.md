# List Identities in Identity Pool

```bash
aws cognito-identity list-identities --identity-pool-id eu-central-1:8bb04998-b1dc-4a0c-b61f-58c3e7e891c4 --max-results 5
```

_Output:_

```bash
{
    "IdentityPoolId": "eu-central-1:8bb04998-b1dc-4a0c-b61f-58c3e7e891c4",
    "Identities": [
        {
            "IdentityId": "eu-central-1:16c0a606-f22f-4138-9f59-76734aa55409",
            "CreationDate": "2022-11-25T14:36:44.171000+01:00",
            "LastModifiedDate": "2022-11-25T14:36:44.171000+01:00"
        },
        {
            "IdentityId": "eu-central-1:2a39ad07-506b-487e-8354-0bcba2db3967",
            "CreationDate": "2022-11-25T14:34:47.251000+01:00",
            "LastModifiedDate": "2022-11-25T14:34:47.251000+01:00"
        }
    ]
}
```

# List IdentityId from Identities

```bash
aws cognito-identity list-identities --identity-pool-id eu-central-1:8bb04998-b1dc-4a0c-b61f-58c3e7e891c4 --max-results 5 | jq '.Identities[0].IdentityId'
```

_Output:_

```bash
"eu-central-1:2a39ad07-506b-487e-8354-0bcba2db3967"
```

# Delete IdentityId from Identities

```bash
aws cognito-identity delete-identities --identity-ids-to-delete eu-central-1:16c0a606-f22f-4138-9f59-76734aa55409
```

_Output:_

```bash
{
    "UnprocessedIdentityIds": []
}
```

## Script for Deleting IdentityId from Identities

```bash
#!/usr/bin/env bash

# ******************************************************************************************
# ************************************ Prerequsities ***************************************
# ******************************************************************************************
# The following script deletes IdentityID from the given Amazon Cognito Identity Pool.
#
# ---> AWS account
# ---> AWS '.aws/config' and '.aws/credentials' must be created in the user's home directory
# ---> Valid AWS credentials
#
# ******************************************************************************************
# ******************************************************************************************
# ******************************************************************************************

IDENTITY_POOL_ID="eu-central-1:8bb04998-b1dc-4a0c-b61f-58c3e7e891c4"

echo "Indentity Pool ID is set to: ${IDENTITY_POOL_ID}"

# List Identity IDs, parse and iterate over the json output, and delete listed IdentityId
# Possible to list max 60 IdentityIds
aws cognito-identity list-identities --identity-pool-id "${IDENTITY_POOL_ID}" --max-results 60  | jq -r '.Identities | .[] | .IdentityId' |
while read -r identityID; do
    echo "Deleting IdentityId: ""${identityID}"""
    aws cognito-identity delete-identities --identity-ids-to-delete "${identityID}" > /dev/null
done

echo "All IdentityIds have been deleted!"
```