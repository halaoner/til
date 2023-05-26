# Working With Binaries

Binary is not executable:
- Alpine docker image does not have `bash` installed by default
- [Starting a shell in Docker an alpine container](https://stackoverflow.com/questions/35689628/starting-a-shell-in-the-docker-alpine-container)
- [How to run a bash script in an alpine container](https://stackoverflow.com/questions/44803982/how-do-i-run-a-bash-script-in-an-alpine-docker-container)

SH SHELL:

```shell
/pre-commit # tflint
/bin/tflint: line 1: syntax error: unexpected "(" (expecting ")")
```


BASH SHELL:

```bash
bash-5.1# tflint
bash: /bin/tflint: cannot execute binary file: Exec format error
```

> The error means that the binary is probably corrupted -  it was fixed by downloading the correct binary file

Linux command `file` tells you what format the downloaded file is:

```bash
/pre-commit # file tfsec-checkgen-linux-arm64
tfsec-checkgen-linux-arm64: ELF 64-bit LSB executable, ARM aarch64, version 1 (SYSV), statically linked, Go BuildID=ZyU1omsNqdEd8TAFtLXj/8o0LnrGT7CVpc2wm_4aQ/ynUFMU7RijqWEXQV1-6Y/1WScHko73JMJZXp8LwEV, stripped
```

Example of a `Dockerfile` on how to install binary file:

```Dockerfile
# Install terragrunt
RUN wget https://github.com/gruntwork-io/terragrunt/releases/download/v0.42.3/terragrunt_linux_amd64 \
    && mv terragrunt_linux_amd64 terragrunt \
    && chmod u+x terragrunt \
    && mv terragrunt /bin \
    && terragrunt --version
```
