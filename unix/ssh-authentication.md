# SSH Authentication

Logging with ssh keys:
- When I want to log in to a server via `ssh`, my public ssh key has to be presented in `.ssh/autorized_keys` on the remote server I want to ssh
- `known_hosts` is a file that contains public ssh keys of remote servers that I have logged in
- `known_hosts` file lets the client authenticate the server, to check that it isn't connecting to an impersonator
- `authorized_keys` file lets the server authenticate the use

## Authentication with a Private `ssh` Key

```bash
ssh -i <path-to-private-key> <user>@<bastion-host-private-ip>
```

Example:

```bash
[ec2-user@ip-10-0-14-209 ~]$ ssh -i runner-manager.pem ec2-user@10.0.142.19