# Today I Learned

> My local knowledgebase

A collection of concise write-ups on small things I learn day to day across a variety of areas.

Inspired by [jbranchaud/til](https://github.com/jbranchaud/til) repository.

---

## Categories

- [AWS](#aws)
- [Unix](#unix)
- [DevOps](#devops)
- [Mac](#mac)

## AWS
- Amazon Cognito
    - [List Identities in Identity Pool](aws/Amazon-Cognito/list-identities.md)
    - [Delete Identities in Identity Pool](aws/Amazon-Cognito/delete-identities.md)
    - [Get AWS Temporary Credentials](/aws/Amazon-Cognito/temporary-credentials.md)
    - [Get AWS Temporary Credentials Flow](/aws/Amazon-Cognito/temporary-credentials-flow.md)
- Amazon DynamoDB
    - [Run DynamoDB in Docker container](/aws/Amazon-DynamoDB/run-dynamodb-locally.md)
    - [Create Table](/aws/Amazon-DynamoDB/dynamodb-create-table.md)
    - [Delete Table](/aws/Amazon-DynamoDB/dynamodb-delete-table.md)
    - [Write Data](/aws/Amazon-DynamoDB/dynamodb-write.md)
    - [Read Data](/aws/Amazon-DynamoDB/dynamodb-read.md)
- AWS Sysmtes Manager Parameter Store
    - [Put Parameter](/aws/AWS-SSM/put-parameter-ssm.md)
- Amazon S3
    - [Pre-signed URL (CLI)](aws/Amazon-S3/s3-pre-signed-url.md)
    - [GET Pre-signed URL For Every Object in S3 (AWS SDK)](/aws/Amazon-S3/pre-signed-url-for-each-object.md)
    - [Copy Files to S3 Bucket](/aws/Amazon-S3/copy-files-to-s3.md)
    - [Download Files from S3 Bucket](/aws/Amazon-S3/download-files-from-s3.md)
    - [_s3 sync_ Command](/aws/Amazon-S3/s3-sync.md)
- Amazon EFS
    - [Mounting EFS](/aws/Amazon-EFS/mounting-efs.md)
- Amazon EC2
    - [Caveats of Spot Instances](/aws/Amazon-EC2/spot-instances.md)
    - [cloud-init](/aws/Amazon-EC2/cloud-init.md)

## Unix
- Shell Script
    - [Array Iteration](/unix/array-iteration.md)
    - [Calling Function From CLI in Bash Script](/unix/call-function-from-script.md)
    - [Script Parameters Handling](/unix/script-parameters-handling.md)
    - [Sharing Environment Variables Between Bash Scripts](/unix/sharing-env-variables.md)
    - [Passing Arguments to Another Script](/unix/passing-arguments-to-script.md)
    - [Calling a Script from the Main Script](/unix/calling-script-from-main-script.md)
    - [Check if Command Failed](/unix/command-exit-code.md)
- [curl command](/unix/curl-command.md)
- [find command](/unix/find-command.md)
- [gpg command](/unix/gpg-command.md)
- [jq command](/unix/jq-command.md)
- [strace command](/unix/trace-command.md)
- [vim command](/unix/vim-command.md)
- [Binary not Found (Symbolic Link)](/unix/binary-not-found.md)
- [SSH Authentication](/unix/ssh-authentication.md)

## DevOps
- Docker
    - [SSH Into A Docker Container](/devops/docker/ssh-into-a-docker-container.md)
    - [Clean Up (containers, images, volumes)](/devops/docker/clean-up.md)
    - [Remove Images Without Tag](/devops/docker/remove-images-without-tag.md)
    - [Debugging Tools](/devops/docker/debugging-tools.md)
    - [Non Executable Binaries](/unix/non-executable-binary.md)
    - [Command Not Found During Docker Build](/devops/docker/command-not-found.md)
    - [docker-machine](/devops/docker/docker-machine.md)
    - [Mounting Docker Volumes](/devops/docker/mounting-volumes.md)
    - [Building Multi-Architecture Docker Images With Buildx](/devops/docker/buildx-installation.md)
    - [Docker Proxy (nexus & nginx)](/devops/docker/docker-proxy.md)
- Git
    - [Push Empty Commit](/devops/git/push-empty-commit.md)
    - [Commit Signing Flow](/devops/git/commit-signing.md)
    - [Commit Verification Flow](/devops/git/commit-verification.md)
- GitLab
    - [Create Access Token](/devops/gitlab/create-access-token-gitlab.md)
    - [Get Access Token](/devops/gitlab/get-access-token-gitlab.md)
    - [Get Statistics From a Project](/devops/gitlab/get-statistics-gitlab.md)
    - [Run GitLab Runner Locally](/devops/gitlab/run-gitlab-runner-locally.md)
    - [GitLab Runner Installation](/devops/gitlab/install-gitlab-runners.md)
    - [GitLab CI/ CD](/devops/gitlab/gitlab-ci-cd.md)
    - [Download GPG Public Key](/devops/gitlab/get-gpg-key.md)
    - [Upload GPG Public Key](/devops/gitlab/put-gpg-key.md)
- Cypress
    - [Cypress Tests Inside a Docker Container](devops/cypress-docker-container.md)
- HashiCorp Vault
    - [HashiCorp Vault in a Docker Contanier](devops/hashicorp-vault.md)
- JFrog
    - [Get Statistics From JFrog Artifactory](/devops/jfrog/get-statistics.md)

## Mac
- [List Open Ports](mac/list-ports.md)

# Contribution

Feel free to open a new issue and a Pull Request if you see a room for improvement.

# License

© 2022-2023 halaoner

This repository is licensed under the [MIT License](https://opensource.org/license/mit/) license. See `LICENSE` for details.
