## [Read](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Scan.html) DynamoDB Table

Read data from DynamoDB that runs locally in a Docker container.

```bash
aws dynamodb scan --table-name <name-of-table> --endpoint-url http://localhost:8000
```

_For example:_

```bash
aws dynamodb scan --table-name GPG-Statistics --endpoint-url http://localhost:8000
```