# gpg command

## Non-interactive trusting of GPG public key 

```bash
echo -e "5\ny\nquit" | gpg --batch --command-fd 0 --expert --edit-key "${PUBLIC_KEY_ID}" trust 2>/dev/null
```

**INFO:**\
`2>/dev/null`

- `2> file` redirects stderr to file
- `/dev/null` is the null device it takes any input you want and throws it away

**Reference:** 
- [Ask Ubuntu](https://askubuntu.com/questions/350208/what-does-2-dev-null-mean)
- [GPG noninteractive batch sign, trust and send gnupg keys](https://raymii.org/s/articles/GPG_noninteractive_batch_sign_trust_and_send_gnupg_keys.html)

## Export masterKeyID in ASCII format

```bash
gpg -a --export "${EMAIL_ADDRESS}" 2>/dev/null | gpg --list-packets --verbose 2>/dev/null | grep 'keyid:' > masterKeyID.txt
```
