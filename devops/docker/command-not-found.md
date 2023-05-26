# Command Not Found During Docker Build

Bash complains during the `docker build` that a specific command was `not found` even though the package, binary or script is presented on the system and it is executable.

Code snippet from a `Dockerfile` build:

```bash
#30 [build 23/26] RUN pmd --version
#30 sha256:2e3dbed058174cf211151672e8f142225ac66ec7f2cad5aac6bc4b5c957f89aa
#30 0.253 /bin/sh: pmd: not found
#30 ERROR: executor failed running [/bin/sh -c pmd --version]: exit code: 127
```

**Error:**

`#30 0.253 /bin/sh: pmd: not found`

## Problem Solved

- If the package is presented, script is executable, binary is in the `$PATH`, check the following:
    - `bash` shell is installed (`alpine` linux distribution uses `ash` shell by default - see [alpine linux wiki](https://wiki.alpinelinux.org/wiki/Change_default_shell).

- If the package/ binary is a shell script (`*.sh`), check the following:
    - the `shebang` - interpreter (e.g., `/bin/bash`) is presented/ installed in the container (`bash` in installed in to the container during `docker build`)

- Every layer in a `Dockerfile`, e.g., `RUN`, `COPY` runs in a **separate shell session** (terminal)
    - for example, when I create `alias p='pwd'` in shell `session 1`, this `alias` will not be presented in the shell `session 2`
