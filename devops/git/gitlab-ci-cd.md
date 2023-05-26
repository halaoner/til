# GitLab CI/ CD Configuration

## Tag

Using `tag` when ensuring that GitLab CI/CD runs on the specific GitLab Runners (e.g., AWS Runner).

> 💡 **INFO** 💡
>
> Enhance `.gitlab-ci.yml` about `tags` keyword to configurre the CI/ CD pipeline to run on AWS GitLab Runners.

Example:

```bash
stages:
  - test

test:
  stage: test
  image: npalm/cowsay
  tags:
    - aws-gitlab-runner

  script:
    - ls -lah
```

> ❗ **IMPORTANT** ❗
>
> Valid AWS credentials are required!