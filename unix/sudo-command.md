# sudo command

## `sudo -i`

The following command clones the repository in the `/data/ci/credentials` directory:


```bash
[RUNNER-PRD]test-user@runner-14:~$ sudo -i git -C /data/ci/credentials pull
remote: Enumerating objects: 7, done.
remote: Counting objects: 100% (7/7), done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 4 (delta 2), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (4/4), 665 bytes | 332.00 KiB/s, done.
From gitlab.mycompany.ch:runner-configuration-internal/gitlab-runner-infrastructure/runner-home
   a89ec86..e19557e  master     -> origin/master
Updating a89ec86..e19557e
Fast-forward
.m2/settings.xml | 3 ++-
1 file changed, 2 insertions(+), 1 deletion(-)
```

- `-C /data/ci/credentials` it specifies the directory where the Git repository is located
- `-i` starts a new shell session with root privileges. It opens a new interactive root shell. That means `/etc/profile` is executed (without `-i` you get non-interactive shell with no profile)

```bash
[RUNNER-PRD]test-user@runner-14:~$ cat /etc/profile.d/devops-team-agent.sh
if [[ -f /opt/devops-team/ssh/id_ed25519 ]]; then
  eval $(ssh-agent) &>/dev/null
  ssh-add <(cat /opt/devops-team/ssh/id_ed25519) &>/dev/null
fi
```
