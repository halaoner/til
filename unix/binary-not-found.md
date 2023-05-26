# Binary not Found (Symbolic link)

When executing a command and getting the following error, even though the binary is installed in the `user` profile (e.g., under `ubuntu` user):

```bash
[root@ip-10-0-142-19 ec2-user]# sudo aws
zsh: command not found: aws
```

- Let's create a symlink that poinst to the `$PATH` environmental variable.
- A symlink (also called a symbolic link) is a type of file in Linux that points to another file or a folder on your computer

**Creating symbolic link to a binary:**

`ln -s source_file symbolic_link`

```bash
ln -s /usr/local/aws-cli/v2/current/bin/aws /bin/aws
```

**Executing binary with a absolute PATH:**

```
[root@ip-10-0-142-19 ec2-user]# /usr/local/aws-cli/v2/current/bin/aws

usage: aws [options] <command> <subcommand> [<subcommand> ...] [parameters]
To see help text, you can run:

  aws help
  aws <command> help
  aws <command> <subcommand> help

aws: error: the following arguments are required: command
```

**Checking the symbolic link for the `aws` binary:**

```bash
[root@ip-10-0-142-19 ec2-user]# ls -lah /bin/ | grep aws
lrwxrwxrwx.  1 root root    37 May 17 13:44 aws -> /usr/local/aws-cli/v2/current/bin/aws

[root@ip-10-0-142-19 ec2-user]# aws

usage: aws [options] <command> <subcommand> [<subcommand> ...] [parameters]
To see help text, you can run:

  aws help
  aws <command> help
  aws <command> <subcommand> help

aws: error: the following arguments are required: command
```
