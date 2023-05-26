# GitLab Runners on AWS EC2

## GitLab Runners Installation

EC2: RHEL distriburion

**Installation** steps are described in the official GitLab documentation - [prepare the runner manager instance](https://docs.gitlab.com/runner/configuration/runner_autoscale_aws/#prepare-the-runner-manager-instance).

> You can user installation steps for CentOS if RHEL does not work.

> ❗ **IMPORTANT** ❗
>
> - Use the following docker-machine version: `docker-machine version 0.16.2-gitlab.15, build f9f7b5f2`
>
> - [docker-machine](https://gitlab.com/gitlab-org/ci-cd/docker-machine/-/blob/main/docs/install-machine.md) installation
>
> - Autoscaling of spot-isntances might not work with the newer version of `docker-machine` as mentioned in the [GitLab issue](https://gitlab.com/gitlab-org/gitlab-runner/-/issues/29213).

**Registration** steps are described in the official GitLab documentation - [registering the GitLab Runner](https://docs.gitlab.com/runner/configuration/runner_autoscale_aws/#registering-the-gitlab-runner).


## GitLab Runners Configuration

Runners configuration is available in on the GitLab Runner Manager in `/etc/gitlab-runner/config.toml`.

> 💡 **INFO** 💡
>
> - `pre_build_script.sh` is mapped and executed from the docker container on the GitLab Runner
>
> - `pre_build_script.sh` is mounted in the root `/` directory, and therefore it must be executed from there:
>
>```bash
>[[runners]]
>   ...
>   ...
>   pre_build_script = "/pre_build_script.sh"
>```

> 💡 **INFO** 💡
>
> Check [cloud-init](/aws/Amazon-EC2/cloud-init.md) when having problems with executing `userdata` script on the GitLab Runner instance.