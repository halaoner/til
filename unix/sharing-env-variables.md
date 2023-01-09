## Sharing Environment Variables Between Bash Scripts

### first-script.sh:

```bash
#!/usr/bin/env bash

UNIQUE_ID="123abc"
export UNIQUE_ID

env | grep UNIQUE_ID
```

### second-script.sh:

```bash
#!/usr/bin/env bash

echo "This is an unique ID: ${UNIQUE_ID}"
```

- You need to `source` the `first-script.sh` to access the `UNIQUE_ID` environment variable in the `second-script.sh`: 

   - `source ./first-script.sh`

- Then, when you execute `./second-script.sh`, the UNIQUE_ID environment variable will be accessible.

### Example

1. Without `sourcing` the `first-script.sh`:

```bash
gpg-key git:(feature/gpg-statistics) ./first-script.sh
UNIQUE_ID=123abc

gpg-key git:(feature/gpg-statistics) ./second-script.sh
This is an unique ID:
```

2. With `sourcing` the `first-script.sh`:

```bash
gpg-key git:(feature/gpg-statistics) source ./first-script.sh
UNIQUE_ID=123abc

gpg-key git:(feature/gpg-statistics) ./second-script.sh
This is an unique ID: 123abc
```