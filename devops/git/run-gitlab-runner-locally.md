# Run GitLab Runner Locally

Code snippet from GitLab CI piepline:
- variable usage
- proper indentation of commands and their arguments in `before_script`

```bash
stages:
  - node
  - maven

variables:
  GO_VERSION: "1.19.4"
  ARCHITECTURE: "amd64"

node-pre-commit:
  image: node:slim
  tags:
    - docker_spot_runner
  stage: node
  # Install dependencies
  before_script:
      - |
        apt-get update
        apt-get install -y \
            git \
            python3-pip \
            shellcheck \
            wget
        pip install \
            pre-commit \
            detect-secrets
        detect-secrets scan > .secrets.baseline
        wget https://go.dev/dl/go${GO_VERSION}.linux-${ARCHITECTURE}.tar.gz
        tar -C /usr/local -xzf go${GO_VERSION}.linux-${ARCHITECTURE}.tar.gz
        rm go${GO_VERSION}.linux-${ARCHITECTURE}.tar.gz
        export PATH=$PATH:/usr/local/go/bin
        go version
        pre-commit --version
        detect-secrets-hook --version
        shellcheck -V
  # Run pre-commit hooks
  script:
    - pre-commit run --all-files
```

Run GitLab-runner `node-pre-commit` stage locally:

```bash
gitlab-runner exec docker node-pre-commit
```