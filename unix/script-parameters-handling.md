# Proper Script Parameters Handling

The code snippet:
- When running the script, `getopts` checks the available parameters/ arguments (available arguments are: `-n`, `-e`, and `-h`).

```bash
while getopts n:e:h? option;do

case${option}in

n)fullName="${OPTARG}";;

e)emailAddress="${OPTARG}";;

h|?)helpMe &&exit 0;;

*)die 90 "invalid option \"${OPTARG}\"";;

esac

done
```
