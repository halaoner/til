# docker-machine 

[docker-machine](https://github.com/docker/machine) lets you create a new virtual Docker host machine. You can run Docker containers on this Docker host machine:

Example:

- EC2 instance (RHEL distribution) --> Installation of `docker-machine` (Docker host virtual instances)
- Running Docker containers on the Docker host machine (docker-machine)
- GitLab CI/CD pipeline can be executed in a Docker container on these Docker host machines (docker-machines)


## GitLab Runners Example

Having GitLab Runner Manager that runs on AWS on EC2 instance according to [Autoscaling GitLab Runner on AWS EC2](https://docs.gitlab.com/runner/configuration/runner_autoscale_aws/).

## Cannot List GitLab Runners (docker-machines)

When running `sudo gitlab-runner start` docker-machine is running as `root`. 

> Make sure that the `docker-machine` binary is in `PATH` of the root user as well.

### Case #1: log in as `ec2-user`

Cannot see `runner-x7pdju-v-gitlab-docker-machine-1683538164-22b850c3` under `ec2-user`.

```bash
[ec2-user@ip-10-0-142-19 ~]$ whoami
ec2-user
[ec2-user@ip-10-0-142-19 ~]$ docker-machine ls
NAME   ACTIVE   DRIVER      STATE     URL                      SWARM   DOCKER    ERRORS
test   -        amazonec2   Running   tcp://10.0.140.32:2376           v23.0.5
```

### Case #2: log in as `root`

```bash
[ec2-user@ip-10-0-142-19 ~]$ sudo su
[root@ip-10-0-142-19 ec2-user]#
[root@ip-10-0-142-19 ec2-user]# whoami
root
[root@ip-10-0-142-19 ec2-user]#
[root@ip-10-0-142-19 ec2-user]# docker-machine ls
NAME                                                        ACTIVE   DRIVER      STATE     URL                      SWARM   DOCKER    ERRORS
runner-x7pdju-v-gitlab-docker-machine-1683538164-22b850c3   -        amazonec2   Running   tcp://10.0.131.81:2376           v23.0.5
```

### Case #3: using `sudo`

```bash
[ec2-user@ip-10-0-142-19 ~]$ whoami
ec2-user
[ec2-user@ip-10-0-142-19 ~]$
[ec2-user@ip-10-0-142-19 ~]$ docker-machine ls
NAME   ACTIVE   DRIVER      STATE     URL                      SWARM   DOCKER    ERRORS
test   -        amazonec2   Running   tcp://10.0.140.32:2376           v23.0.5
[ec2-user@ip-10-0-142-19 ~]$
[ec2-user@ip-10-0-142-19 ~]$
[ec2-user@ip-10-0-142-19 ~]$ sudo docker-machine ls
NAME                                                        ACTIVE   DRIVER      STATE     URL                      SWARM   DOCKER    ERRORS
runner-x7pdju-v-gitlab-docker-machine-1683538164-22b850c3   -        amazonec2   Running   tcp://10.0.131.81:2376           v23.0.5
```

## List `docker-machine`

**List** docker-machines by executing `sudo docker-machine ls` on the GitLab Runner Manager.

```bash
[ec2-user@ip-10-0-142-19 ~]$ sudo docker-machine ls
NAME                                                        ACTIVE   DRIVER      STATE     URL                       SWARM   DOCKER    ERRORS
runner-x7pdju-v-gitlab-docker-machine-1683734514-88349d7a   -        amazonec2   Running   tcp://10.0.139.158:2376           v23.0.6
```

## SSH to a `docker-machine`

**Connect** to a docker-machine by executing `sudo docker-machine ssh <runner-name>` on the GitLab Runner Manager.

```bash
[ec2-user@ip-10-0-142-19 ~]$ sudo docker-machine ssh runner-x7pdju-v-gitlab-docker-machine-1683734514-88349d7a
Welcome to Ubuntu 20.04.4 LTS (GNU/Linux 5.13.0-1022-aws x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Thu May 11 07:44:25 UTC 2023

  System load:  0.0                Processes:                117
  Usage of /:   27.1% of 15.45GB   Users logged in:          0
  Memory usage: 34%                IPv4 address for docker0: 172.17.0.1
  Swap usage:   0%                 IPv4 address for eth0:    10.0.139.158

 * Ubuntu Pro delivers the most comprehensive open source security and
   compliance features.

   https://ubuntu.com/aws/pro

64 updates can be applied immediately.
To see these additional updates run: apt list --upgradable

New release '22.04.2 LTS' available.
Run 'do-release-upgrade' to upgrade to it.


*** System restart required ***
Last login: Thu May 11 07:16:04 2023 from 10.0.142.19
ubuntu@runner-x7pdju-v-gitlab-docker-machine-1683734514-88349d7a:~$ whoami
ubuntu
ubuntu@runner-x7pdju-v-gitlab-docker-machine-1683734514-88349d7a:~$ hostname
runner-x7pdju-v-gitlab-docker-machine-1683734514-88349d7a
```