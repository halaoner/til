## [Write](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/getting-started-step-2.html) Data to DynamoDB Table

Write data in to DynamoDB that runs locally in a Docker container.

Write static data:

```bash
aws dynamodb put-item \
    --table-name Statistics  \
    --item \
        '{"KeyID": {"N": "0002"},"Key": {"S": "anothergpg--key-test67890!@£?>"}, "Timestamp": {"N": "20221211021725"}}' \
    --endpoint-url http://localhost:8000
```

or write new item by using environmental variables:

```bash
aws dynamodb put-item \
    --table-name Statistics  \
    --item \
        '{"KeyID": {"N": "0003"},"Key": {"B": '\"$KEY\"'}, "Timestamp": {"N": '\"$TIME\"'}}' \
    --endpoint-url http://localhost:8000
```