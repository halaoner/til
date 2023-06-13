# Get GPG Public Key from a User

Download a GPG public key from a particular user:

```bash
curl \
    -s \
    -X GET \
    --header "PRIVATE-TOKEN: ACCESS_TOKEN" "https://gitlab.com/api/v4/users/0123/gpg_keys" | jq '[.[].key]'
[
  "-----BEGIN PGP PUBLIC KEY BLOCK-----\r\n\r\nmDMEYuOrfxYJKwYBBAH2dw8BAQdAuaA85naDsJJ6TIOutnRgYU09f/A6UimfiJeF\r\nhyNopM+0OE9uZHJlaiBIYWxhc2thIChHaXRMYWItR1BHLWtleSkgPG9uZHJlai5o\r\nYWxhc2thQHRpOG0uY2g+iJMEExYKADsWIQQmVR9n1+1ul/8IZ5qv21s9BCa5KQUC\r\nYuOrfwIbAwULCQgHAgIiAgYVCgkICwIEFgIDAQIeBwIXgAAKCRCvVFs9BCa5KVu3\r\nAQCa1fTRDiOg+uBjqnZ8tBjcIQ7mR+IPfmU0nl8JncUHWAEAzl8FZAwY1Z12LsLD\r\n3YF/zapI0UR+a2fL9y4l+9477gW4OARi46t/EgorBgEEAZdVQQUBAQdALJl364LF\r\nWRsjmagk03lhSknnUItHmByg/6XR83FwJCUDAQgHiHgEGBYKACAWIQQmVR9n1+1u\r\nl/8IZ5qvVFs9BCa5KQUCYuOrfwIbDAAKCRCvVFs9BCa5KZzUAQDlEWoeMLUV/l7s\r\nP3jOj52QmiEXq9fW/YughtCxZPdBywD/fzF4texy5gJYaaZuoxtnOLleKyiFXexZ\r\n7OHSxArQ9AU=\r\n=IUIz\r\n-----END PGP PUBLIC KEY BLOCK-----"
]
```

## Get only active users

```bash
jq '[.[]|select(.state=="active")]'
```