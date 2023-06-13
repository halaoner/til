# Upload GPG Public Key

Upload a GPG public key of a particular user to the GitLab account:

```bash
curl \
    --silent \
    --location \
    --request POST "https://gitlab.com/api/v4/user/gpg_keys" \
    --header "PRIVATE-TOKEN: ${ACCESS_TOKEN}" \
    --form 'key="-----BEGIN PGP PUBLIC KEY BLOCK-----
    '"$GPG_PUBLIC_KEY"'
    -----END PGP PUBLIC KEY BLOCK-----"' | jq '.[] | {key, fingerprint}'
```

GPG Public Key

```bash
GPG_PUBLIC_KEY=
-----BEGIN PGP PUBLIC KEY BLOCK-----

mDMEYtAGPBYJKwYQQAHaRw8BAQdATb96IfxN1sPQJ7LdvJ8bbntFKQ4MbHan7uam
0rrnOeK0K0RhbmllbCBFc3Rlcm1hbm4gPGRhbmllbC5lc3Rlcm1hbm5AdGk4bS5j
aD6ImQQTFgoAQRYhBOqCHrSxECtc1g6IQfd07cg3a/gWBQJi0AY8AhsDBQkDwmcA
BQsJCAcCAiICBhUKCQgLAgQWAgMBAh4HAheAAAoJEPd07cg3a/gWHYQA/jJHgSGe
VROmV4VGO7RfcZbUyx3ucNFFhljHUkzNTZklAQCO/moQdVaSLo4plw5AbiHuciKt
0wyOtEnMCTamwPo8CLg4BGLQBjwSCisGAQQBl1UBBQEBB0C6PE+x5NpSOneQIK9J
gvogygqdDE2Y0ankv0+HAnJVIAMBCAeIfgQYFgoAJhYhBOqCHrSxECtc1g6IQfd0
7cg3a/gWBQJi1QaAY8AhsMBQkDwmcAAAoJEPd07cg3a/gWbegBAI5/QAtOlSB/uG
t1CewSKSFPDoT8GwJkE4ts7U3yA2AQC/o1wUKUWKUbZGzsoAVu2xq2NlECPoCC3e
omu8qXttCQ==
=/qSS
-----END PGP PUBLIC KEY BLOCK-----
```