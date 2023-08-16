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
```

## Cannot SSH into an Instance

You can face the error below when a SSH fingerprint changed.

```bash
[ec2-user@ip-10-35-0-59 ~]$ ssh -i nexus-gui.pem ec2-user@10.35.0.100
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that a host key has just been changed.
The fingerprint for the ED25519 key sent by the remote host is
SHA256:2D09myg2Qzu9ldbdWNsxkNbq3CpDpoMnfAZhLq12OJE.
Please contact your system administrator.
Add correct host key in /home/ec2-user/.ssh/known_hosts to get rid of this message.
Offending ECDSA key in /home/ec2-user/.ssh/known_hosts:3
Host key for 10.35.0.100 has changed and you have requested strict checking.
Host key verification failed.
```

- it is because the instance has an SSH key --> when you delete the instance, create a new one --> the new instance will have a different SSH fingerprint, that does not match with the one you have in `.ssh/known_hosts` file

```bash
[ec2-user@ip-10-35-0-59 ~]$ cat .ssh/known_hosts
10.35.0.100 ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIAs2vgcg9dJLBJpjJiUiaQU0wSdHvqGglFnMBqVS1Liy
10.35.0.100 ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDYDoJ9PZ6gR/QHqR67ZWeumV2tugF6bDqbhHv9mkId3bKmIvrVtfFO+EzrUi9gwtVI4AJGwqZMUrtVLVQM8FHfkeBRA6MEW+2QY7TacOJeYWSiq4eeGty6UVAH68NLNMr4etiBlQOUNLoocSqwvVN7uL8tGt0XL0lNZq05LKs+eOKtixH3ag7i1up1jR2IJx/pAiz0afSLP0VCsNDzT9TWZSF/CjaS6+eyLoh/BRK6aYqXBlAK7y4XWEdBg0sNmwxwbFbQCAAs0wTvapC89thSLmq1Kz0wEGBDb7myd0dhiJr6GGRF3cbI2Qrk66pFeCNBcz2CyjoyySXeIHU/B60n
10.35.0.100 ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBE9GlfxFrqmbj1oh7nOqAZWZ4VK6E8eJ0Kl0X03jrEX2rfc645ohq1Rmk4OBlb39xMIIF6/0iCD2fMIq3HkP25k=
```

- rename the `.ssh/known_hosts` file and the ssh again and it will work

```bash
[ec2-user@ip-10-35-0-59 ~]$ mv .ssh/known_hosts .ssh/known_hosts.old2
```

- connect to the instance again

```bash
[ec2-user@ip-10-35-0-59 ~]$ ssh -i nexus-gui.pem ec2-user@10.35.0.100
The authenticity of host '10.35.0.100 (10.35.0.100)' can't be established.
ED25519 key fingerprint is SHA256:2D09myg2Qzu9ldbdWNsxkNbq3CpDpoMnfAZhLq12OJE.
This key is not known by any other names
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.35.0.100' (ED25519) to the list of known hosts.
Last login: Mon Jul 17 11:11:18 2023 from 212-51-132-169.fiber7.init7.net

       __|  __|_  )
       _|  (     /   Amazon Linux 2 AMI
      ___|\___|___|

https://aws.amazon.com/amazon-linux-2/
11 package(s) needed for security, out of 11 available
Run "sudo yum update" to apply all updates.
```

- now you can check the new ssh fingerprints

```bash
[ec2-user@ip-10-35-0-59 ~]$ cat .ssh/known_hosts
10.35.0.100 ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAICJfkrxeWlX+uZ/varpMVUvbflBPS7lCSnS/Y5cmzLlZ
10.35.0.100 ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDSV8qxlrRRfTkFlUPA5V/Xo0vV0O59fsHORiWiV9hezJ3I8JDDXZ02mBVCDOlZ9xiIOMVvWPGwr7SXMk74+Yy8s8JGjwfckcV2RULyov7hyOpvs9pkNAy8V6V0aO7pjqZ/qmt8kne9ysma2YgYnQA16vFIpDc3CV+dckUdUEVVNjJf+slXl4kbnt2iHehMptZhwdYsVXtFULVsSjCSOKhvNk6yztYAHTU/d5bspabdYXxRcler4JB+ZLX9A83q02GH81f8kEpCxePXVerDtNSYZufOLTVCMWeaF89ovMnuzB4rep1TTcDlCvikE5BNv2p3C1uyK1kGPs3D02Pdsv13
10.35.0.100 ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBIwcmJgtP1FssrIpS10kZ2WpAUxVUq6scgeTXj4lUbV646X+gbZc6zxSGmdlxA5cYNj1nUDc20luWnzra547VkI=
```

