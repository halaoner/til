# Array Iteration

The following code snipped iterates over an array until the last index of the array.

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