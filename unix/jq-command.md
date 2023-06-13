# jq command

`jq` command **without** `-r` argument:

```bash
cat gpg-public-key.json | jq '.[]'
"-----BEGIN PGP PUBLIC KEY BLOCK-----\r\n\r\nmDMEYtAGPBYJKwYBBAHaRw8BAQdATb96IfWW1sPQJ7LdvJ8bbntFKQ4MbHan7uam\r\n0rrnOeK0K0RhbmllbCBFc3Rlcm1hbm4gPGRhbmllbC5lc3Rlcm1hbm5AdGk4bS5j\r\naD6ImQQTFgoAQRYhBOqCHrSxECtc1g6IQfd07cg3a/QWBQJi0AY8AhsDBQkDwQQA\r\nBQsJCAcCAiICBhUKCQgLAgQWAgMBAh4HAheAAAoJEPd07cg3a/gWHYQA/jJHgSGe\r\nVROmV4VGO7RfcZbUyx3ucNQNhljHUkzNTZklAQCO/moQdVaSLo4plw5AbiHuciKt\r\n0wyOtEnMCTamwPo8CLg4BGLQBjwSCisGAQQBl1UBBQEBB0C6PE+x5NpSOneQIK9J\r\ngffgygqdDE2Y0ankv0+HAnJVIAMBCAeIfgQYFgoAJhYhBOqCHrSxECtc1g6IQfd0\r\n7cg3a/gWBQJi0AY8AhsMBQkDwmcAAAoJEPd07cg3a/gWbegQQI5/QAtOlSB/uG69\r\nt1CewSKSFPDoT8GwJkE4ts7U3yA2AQC/o1wUKUWKUbZGzsoAVu2xq2NlECPoCC3e\r\nomu8qXttCQ==\r\n=/qSS\r\n-----END PGP PUBLIC KEY BLOCK-----"
```

`jq` command **with** `-r` argument:

```bash
cat 4567-123-gpg-public-key.json | jq -r '.[]'
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

**EXPLAINED:**\
The `-r` option ensures that the output is shown as raw strings rather than JSON-encoded strings.\
The `.` (dot) represents the entire JSON document as the filter for processing.