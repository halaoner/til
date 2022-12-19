## [Delete](https://amazon-dynamodb-labs.com/hands-on-labs/explore-cli/cli-deleting-data.html) DynamoDB Table

Delete a table from DynamoDB that runs locally in a Docker container.

```bash
aws dynamodb delete-table --table-name <name-of-table> --endpoint-url http://localhost:8000
```

_For example:_

```bash
aws dynamodb delete-table --table-name GPG-Statistics --endpoint-url http://localhost:8000
```