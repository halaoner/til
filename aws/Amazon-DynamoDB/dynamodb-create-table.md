
## [Create](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/getting-started-step-1.html) DynamoDB Table 

Create a table in to DynamoDB that runs locally in a Docker container.

[AWS DynamoDB Attribute Data Types](https://usefulangle.com/post/332/dynamodb-attribute-types)

```
aws dynamodb create-table \
    --table-name Statistics \
    --attribute-definitions \
        AttributeName=KeyID,AttributeType=N \
        AttributeName=ey,AttributeType=B \
    --key-schema \
        AttributeName=KeyID,KeyType=HASH \
        AttributeName=Key,KeyType=RANGE \
    --provisioned-throughput \
        ReadCapacityUnits=5,WriteCapacityUnits=5 \
    --table-class STANDARD \
    --endpoint-url http://localhost:8000
```

**NOTE:** [DynamoDB-Adding non key attributes](https://stackoverflow.com/questions/38151687dynamodb-adding-non-key-attributes)