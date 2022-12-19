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