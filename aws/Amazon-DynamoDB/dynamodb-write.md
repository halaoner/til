## [Write](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/getting-started-step-2.html) Data to DynamoDB Table

Write data in to DynamoDB that runs locally in a Docker container.

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