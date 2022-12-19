# How To Call Bash Script Function From CLI

Calling function `checkForInstalledGPG` from the bash script from CLI:

```bash
enhancements git:(feature/gpg-key) source ./test.sh; checkForInstalledGPG
```

Or (`checkForExistingGPG` function requires parameters `name` and `email`)

```bash
enhancements git:(feature/gpg-key) source ./test.sh; checkForExistingGPG "John Reed" "john.reed@gmail.com"
```
