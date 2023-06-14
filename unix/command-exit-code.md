# Condition if Command Failed

```bash
#!/usr/bin/env bash

USER_ID=123
USER_NAME="Peter Pan"

set -x

if cat key.json | gpg --import; then
    echo "GPG public key for USER_ID: ${USER_ID} and USER_NAME: '${USER_NAME}' imported to a keyring."
else
    echo "Invalid GPG public key format USER_ID: ${USER_ID} and USER_NAME: '${USER_NAME}'"
fi
```


**Explained**:
1. `cat key.json` reads the contents of the `key.json` file.
2. The pipe (`|`) symbol sends the output of `cat key.json` as input to the `gpg --import` command.
3. `gpg --import` imports the GPG public key from the input into a keyring.

- If the `gpg --import` command is **successful** (returns a zero exit status), meaning the GPG public key is imported successfully, then the code block following the `then` keyword is executed.
- It prints a message indicating that the GPG public key for a specific `USER_ID` and `USER_NAME` has been imported to the keyring.

_Output from the script:_

```bash
+ USER_ID=123
+ USER_NAME='Peter Pan'
+ cat key.json
+ gpg --import
gpg: key A443DB9C703B192F: "Peter Pan (GPG key: GitLab key) <peter.pan@gmail.com>" not changed
gpg: Total number processed: 1
gpg:              unchanged: 1
+ echo 'GPG public key for USER_ID: 123 and USER_NAME: '\''Peter Pan'\'' imported to a keyring.'
GPG public key for USER_ID: 123 and USER_NAME: 'Peter Pan' imported to a keyring.
```

- If the `gpg --import` command **fails** (returns a non-zero exit status), indicating an error occurred during key import, the code block following the `else` keyword is executed.
- It prints a message stating that the GPG public key has an invalid format for the given `USER_ID` and `USER_NAME`.

_Output from the script:_

```bash
+ USER_ID=123
+ USER_NAME='Peter Pan'
+ cat key.json
+ gpg --import
gpg: invalid armor header: mQMEYyRIPhzJKqYBBAHaRw8BAQdA5WY4vyS8I8sApw6zMPfZd2qqZSst2R55VGZO\n
gpg: key A443DB9C703B192F: "Peter Pan (GPG key: GitLab key) <peter.pan@gmail.com>" not changed
gpg: Total number processed: 1
gpg:              unchanged: 1
+ echo 'Invalid GPG public key format USER_ID: 123 and USER_NAME: '\''Peter Pan'\'''
Invalid GPG public key format USER_ID: 123 and USER_NAME: 'Peter Pan'
```
