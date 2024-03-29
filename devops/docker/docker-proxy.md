# Docker Proxy (nexus & nginx)

**Use case #1**

Having a GitLab Runner that runs on EC2 on AWS. First, the GitLab Runner checks the Nexus Docker Proxy (communication goes via Nginx Reverse Proxy in case of pulling Docker image from the on-prem GitLab container registry) whether a particular Docker image is presented, and pulls it from there (if the Docker image is cached). If the Docker image is not presented in the cache ([Nexus Repository Manager](https://help.sonatype.com/repomanager3/nexus-repository-administration/formats/docker-registry/proxy-repository-for-docker)), Nexus Docker Proxy pulls the Docker image either from the on-prem GitLab container registry or Docker Hub.

[Nginx Reverse Proxy](https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/) is used for proxying HTTP requests for `docker pull gitlab.int.com:5043` (from the GitLab Runner) to Nexus Docker Proxy that is configured with the remote GitLab container registry URL (`https://gitlab.int.com:5043`) and Docker Hub URL (`https://registry-1.docker.io`).

> - `gitlab.int.com` should be resolved to IP for a machine, where the Nginx runs
>
> - a DNS record in `/etc/hosts` like `127.0.0.1 gitlab.int.com` has to be created on the machine where **Nginx runs**
>
> - a DNS record in `/etc/hosts` like `10.35.0.88 gitlab.int.com` on the **GitLab Runner** has to be created that points to the Nginx Reverse Proxy
>
> - `https://gitlab.int.com:5043` on the **Nexus Docker Proxy** points to the actual on-prem GitLab container registry

_This configuration is done because it was a **requirement** NOT to interfere the CI pipeline configuration. Therefore, `gitlab.int.com` DNS record points to the Nginx Reverse Proxy (on the GitLab Runner) that proxying `gitlab.int.com` to the Nexus Docker Proxy (and not directly to on-prem GitLab instance) that is passing the requests to the actual on-prem GitLab._

> ❗ **IMPORTANT** ❗ 
>
> There can be a problem with for example, clonning a GitLab repository or Docker login command when modifying DNS records in `/etc/hosts`

## _Flow of the `docker pull gitlab.int.com` request_

HTTP request `docker pull gitlab.int.com:5043/secret-docker-image:1.0` from GitLab Runner ➡️ Nginx Reverse Proxy ➡️ Nexus Docker Proxy ➡️ on-prem GitLab

## _Flow of the `docker pull docker.io` request_

HTTP request `docker pull docker.io/library/alpine` from GitLab Runner ➡️ Nexus Docker Proxy ➡️ Docker Hub

The diagram below represents the solution, including the **important** parameters snaphosts from the configuration.

![nexus-nginx-proxy](/devops/docker/diagrams/nexus-and-nginx.png)

**Use case #2**

Use Docker proxy on the Docker daemon level and **avoid** to change DNS name in `/etc/hosts`.

Configure `HTTP_PROXY` and `HTTPS_PROXY` variables that point to the Nexus Repository Manager.

Nexus is configured in a way that `Docker Registry Group` consolidates every single Docker regitry (GitLab INT, GitLab, Artifactory INT and Docker Hub) and expose them under one single port `8181` for the whole group. It is up to Nexus Reposiory Manager to forward traffic to a particular Docker registry (remote URL).

The diagram below represents the solution, including the important parameters snaphosts from the configuration.

![nexus-proxy](/devops/docker/diagrams/nexus.png)

