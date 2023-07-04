# vim editor

## Display Line Numbers

1. Open `vim` editor

```bash
sudo vi /etc/gitlab-runner/config.toml
```
2. `:set number` and press ENTER

_`config.toml` code snippet:_

```bash
"/etc/gitlab-runner/config.toml" 327L, 11390B
      1 concurrent = 21
      2 check_interval = 0
      3 log_level = "debug"
      4
      5 #######################################################
      6 ################### AWS GitLab Runner 1 ###############
      7 #######################################################
      8
      9 [[runners]]
     10   name = "aws-gitlab-runner-1"
     11   url = "https://gitlab.com"
     12   id = 2643
     13   token = "REGISTRATION_TOKEN"
     14   token_obtained_at = 2023-05-23T12:02:41Z
     15   token_expires_at = 0001-01-01T00:00:00Z
     16   executor = "docker+machine"
     17   limit = 3
     18   pre_build_script = "/pre_build_script.sh"
     19   [runners.docker]
     20     image = "docker:18.03.1-ce"
     21     privileged = false
     22     disable_entrypoint_overwrite = false
     23     disable_cache = false
     24     volumes = [
     25       "/mnt/s3/.yarnrc.yml:/.yarnrc.yml:ro",
     26       "/mnt/s3/.m2:/.m2:rw",
     27       "/mnt/s3/.docker:/.docker:ro",
     28       "/mnt/s3/.gradle:/.gradle:ro",
     29       "/mnt/s3/.netrc:/.netrc:ro",
     30       "/mnt/s3/.npmrc:/.npmrc:ro",
     31       "/mnt/s3/.ssh/known_hosts:/.ssh_known_hosts:ro",
     32       "/mnt/s3/.ssh:/.ssh:ro",
     33       "/mnt/s3/.team-config:/.team-config:ro",
     34       "/mnt/s3/pre_build_script.sh:/pre_build_script.sh:ro",
     35       "/root/.docker/buildx:/root/.docker/buildx:rw",
     36       "/var/run/docker.sock:/var/run/docker.sock:ro"
     37       ]
     38       extra_hosts = [
     39         "jfrog.com:10.10.40.59",
     40         "jira.com:10.10.40.42",
     41         "sonar-qube.com:10.10.40.29"
     42       ]
:set number
```

## Delete Multiple Lines

1. [Display line numbers](#display-line-numbers)

2. Select lines you want to delete (`vim` is still open) and press ENTER

_`config.toml` code snippet:_

```bash
"/etc/gitlab-runner/config.toml" 327L, 11390B
      1 concurrent = 21
      2 check_interval = 0
      3 log_level = "debug"
      4
      5 #######################################################
      6 ################### AWS GitLab Runner 1 ###############
      7 #######################################################
      8
      9 [[runners]]
     10   name = "aws-gitlab-runner-1"
     11   url = "https://gitlab.com"
     12   id = 2643
     13   token = "REGISTRATION_TOKEN"
     14   token_obtained_at = 2023-05-23T12:02:41Z
     15   token_expires_at = 0001-01-01T00:00:00Z
     16   executor = "docker+machine"
     17   limit = 3
     18   pre_build_script = "/pre_build_script.sh"
     19   [runners.docker]
     20     image = "docker:18.03.1-ce"
     21     privileged = false
     22     disable_entrypoint_overwrite = false
     23     disable_cache = false
     24     volumes = [
     25       "/mnt/s3/.yarnrc.yml:/.yarnrc.yml:ro",
     26       "/mnt/s3/.m2:/.m2:rw",
     27       "/mnt/s3/.docker:/.docker:ro",
     36       "/var/run/docker.sock:/var/run/docker.sock:ro"
     37       ]
     38       extra_hosts = [
     39         "jfrog.ch:10.10.40.59",
     40         "jira.ch:10.10.40.42",
     41         "sonar-qube.ch:10.10.40.29"
     42       ]
:5;7d
```

_Output:_

```bash
"/etc/gitlab-runner/config.toml" 327L, 11390B
      1 concurrent = 21
      2 check_interval = 0
      3 log_level = "debug"
      4
      5
      6 [[runners]]
      7   name = "aws-gitlab-runner-1"
      8   url = "https://gitlab.com"
    ...
    ...
    ...
```

