# Amazon DynamoDB - CRUD Operations

The following sections describe how to execute CRUD (Create, Read, Update, Delete) operations against local DynamoDB running in a Docker container.

## Run DynamoDB Locally in Docker Container

How to run DynamoDB [locally](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/DynamoDBLocal.html).

```bash
docker run -p 8000:8000 amazon/dynamodb-local
```

## [Create](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/getting-started-step-1.html) DynamoDB Table 

[AWS DynamoDB Attribute Data Types](https://usefulangle.com/post/332/dynamodb-attribute-types)

```
aws dynamodb create-table \
    --table-name GPG-Statistics \
    --attribute-definitions \
        AttributeName=PublicKeyID,AttributeType=N \
        AttributeName=PublicKey,AttributeType=B \
    --key-schema \
        AttributeName=PublicKeyID,KeyType=HASH \
        AttributeName=PublicKey,KeyType=RANGE \
    --provisioned-throughput \
        ReadCapacityUnits=5,WriteCapacityUnits=5 \
    --table-class STANDARD \
    --endpoint-url http://localhost:8000
```

**NOTE:** [DynamoDB-Adding non key attributes](https://stackoverflow.com/questions/38151687dynamodb-adding-non-key-attributes)

## [Read](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Scan.html) DynamoDB Table

```bash
aws dynamodb scan --table-name <name-of-table> --endpoint-url http://localhost:8000
```

_For example:_

```bash
aws dynamodb scan --table-name GPG-Statistics --endpoint-url http://localhost:8000
```

## [Delete](https://amazon-dynamodb-labs.com/hands-on-labs/explore-cli/cli-deleting-data.html) DynamoDB Table

```bash
aws dynamodb delete-table --table-name <name-of-table> --endpoint-url http://localhost:8000
```

_For example:_

```bash
aws dynamodb delete-table --table-name GPG-Statistics --endpoint-url http://localhost:8000
```

## [Write](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/getting-started-step-2.html) Data to DynamoDB Table

Write static data:

```bash
aws dynamodb put-item \
    --table-name GPG-Statistics  \
    --item \
        '{"PublicKeyID": {"N": "0002"},"PublicKey": {"S": "anothergpg-public-key-test67890!@£?>"}, "Timestamp": {"N": "20221211021725"}}' \
    --endpoint-url http://localhost:8000
```

or write new item by using environmental variables:

```bash
aws dynamodb put-item \
    --table-name GPG-Statistics  \
    --item \
        '{"PublicKeyID": {"N": "0003"},"PublicKey": {"B": '\"$PUBLICKEY\"'}, "Timestamp": {"N": '\"$TIME\"'}}' \
    --endpoint-url http://localhost:8000
```
