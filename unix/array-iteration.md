# Array Iteration

The following code snipped iterates over an array until the last index of the array.

## Option 1

```bash
COUNT=2
# Get length of the file
ARRAY_LENGTH=$(< array.txt wc -l | xargs)

# Iterate over the array
while (( "${COUNT}" < "${ARRAY_LENGTH}" || "${COUNT}" == "${ARRAY_LENGTH}" ))
do

    echo "Do something here...."

    # Increase $COUNT about number 1
    ((COUNT++ )) || true
done
```

## Option 2

1. script gets `USER_ID` from `${PROJECT_ID}-users.json`
2. script forwards `USER_ID` for the beginning of the while loop
3. while loops is terminated when there are not more records in `${PROJECT_ID}-users.json`

```bash
#!/usr/bin/env bash

set -xe

while read USER_ID ; do 
    FULL_USER_NAME=$(jq -r '.[] | select(.id=='${USER_ID}') | .name' ${PROJECT_ID}-users.json)
    USER_NAME=$(jq -r '.[] | select(.id=='${USER_ID}') | .name' ${PROJECT_ID}-users.json)
    echo "Full username --->" $FULL_USER_NAME
    echo "user_name --->" $USER_NAME
    # Any further steps here...
done < <(jq -r '.[].id' ${PROJECT_ID}-users.json)
```

_Output:_

```bash
+ read USER_ID
+ echo 'user ID --->' 123
user ID ---> 123
++ jq -r '.[] | select(.id==123) | .name' 3456-users.json
+ FULL_USER_NAME='Pan Peter'
++ jq -r '.[] | select(.id==123) | .username' 3456-users.json
+ USER_NAME=pap
+ echo 'Full username --->' Pan Peter
Full username ---> Pan Peter
+ echo 'user_name --->'Pan Pater
user_name ---> pap
```
