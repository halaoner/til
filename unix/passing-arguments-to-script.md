# How To Run Binary/ Command That Requires an Argument

The given scenario:

> I need to install `pmd` package in to a Docker container (`alpine` distribution) and make `pmd` binary executable.
>
> I need to execute a script that accepts an argument.

1. PMD package (binary) is executed as `script.sh arg1` - see [PMD documentation](https://pmd.sourceforge.io/pmd-6.53.0/pmd_userdocs_installation.html#running-pmd-via-command-line):

```bash
run.sh pmd
```

2. I cannot create a [symbolic link](https://www.freecodecamp.org/news/symlink-tutorial-in-linux-how-to-create-and-remove-a-symbolic-link/) to `script.sh arg1`:

```bash
ln -s /pre-commit-config/run.sh pmd /usr/local/bin/pmd
```

3. I can create only the symbolic link as follows (without `arg1`):

```bash
ln -s /pre-commit-config/run.sh /usr/local/bin/pmd
```

4. I need to create a wrapper that allows to pass an argument to a script `script.sh arg1`

- given `pmd.sh` script:

```bash
#!/bin/bash

pmd-bin-6.53.0/bin/run.sh pmd "$@"
```

> 💡 INFO 💡
>
>  `"$@"` (a special parameter) allows to pass a given `argument` to another script
>
> Then, I can execute, for example: `./pmd.sh --version` or `./pmd.sh --help`
>
> This is useful when you want to pass all the arguments passed to the script `pmd` to another script `run.sh` that is being called from the `pmd script`, so in this case, `run.sh` will receive the same arguments as pmd script.
>
> For example, if you run `pmd arg1`, the script `run.sh` will receive the arguments `arg1` when it is called by the `script pmd`.

```bash
#!/bin/bash

pmd-bin-6.53.0/bin/run.sh pmd
```
> 💡 INFO 💡
>
> I cannot execute, for example: `./pmd.sh --version` or `./pmd.sh --help` without `"$@"`.


5. Now, I can execute script `pmd.sh` with `arg1`:

```bash
./pmd.sh --version
PMD 6.53.0
```

> 💡 INFO 💡
>
>  I can pass the argument `--version` because of `"$@"` in the `pmd.sh`.

6. Now, I can create the symbolic link:

`ln -s <path to the file to be linked> <the path of the link to be created>`

```bash
ln -s /pre-commit-config/pmd.sh /usr/local/bin/pmd
```

- mapping ` /pre-commit-config/pmd.sh` to `/usr/local/bin/pmd`
- `pmd` binary points to the `pmd.sh` script --> `/pre-commit-config/pmd.sh`
- now you are able to run `pmd` from anywhere in the shell
- you can check the create symbolic link:

```bash
/pre-commit # ls -lah /usr/local/bin
total 12K
drwxr-xr-x    1 root     root        4.0K Jan 20 14:14 .
drwxr-xr-x    1 root     root        4.0K Aug  9 08:49 ..
lrwxrwxrwx    1 root     root          25 Jan 20 14:14 pmd -> /pre-commit-config/pmd.sh
```

7. Executing `pmd` from anywhere in the shell:

```bash
pmd --version
PMD 6.53.0
```
