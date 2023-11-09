# Nginx Reverse Proxy

Configure NGINX as a reverse proxy for HTTP and other protocols, with support for modifying request headers.

## Use Case No: 1

- Caching Docker images on AWS for GitLab Runners by leveraging [Nexus Free Tier](https://help.sonatype.com/repomanager3/nexus-repository-administration/formats/docker-registry/proxy-repository-for-docker).
- Pushing Docker images to on-prem Artifactory and GitLab Container Registry.
- Nexus Free Tier does not allow to push Docker images to the [groups](https://mtijhof.wordpress.com/2018/07/23/using-nexus-oss-as-a-proxy-cache-for-docker-images/) under the exposed port, e.g., `8181`.
    - The goal is NOT to have Docker images in Nexus but in Artifactory and GitLab.
    - Nexus is used for caching Docker images on AWS close to the GitLab Runners that are deployed on AWS as well.
- Two different Docker credentials:
    - `docker pull` --> credentials for Nexus
    - `docker push` --> credentials for Artifactory and GitLab
- New configuration for the nginx as a reverse proxy is created in `/etc/nginx/conf.d/reverse-proxy.conf`.

![Nginx Reverse Proxy](/devops/nginx/diagrams/nginx-reverse-proxy.png)

[ngx_http_map_module](https://nginx.org/en/docs/http/ngx_http_map_module.html) can be used to forward HTTP requests according to a specific pattern by leveraging the [embedded variables](https://nginx.org/en/docs/http/ngx_http_core_module.html#variables). 
The following example uses:
- `$request_method`
- `$remote_user`
- `$host`
- `$args`


The `$docker_destination` (an upstream server where the traffic is forwarded) is not logged by default but the nginx log format can be enhanced - see [enhanced logging](/devops/nginx/enhance-logging.md).

> ❗ **NOTE:** ❗
>
> Make sure that the rules do not clash between each other.
>
> Make sure you understand the priority of the rules according to the nginx logic - see [here](https://nginx.org/en/docs/http/ngx_http_map_module.html) and [here](https://stackoverflow.com/questions/1011101/nginx-location-directive-doesnt-seem-to-be-working-am-i-missing-something).

```
map "$request_method:$remote_user:$host:$args" $docker_destination {

    # If GET method and remote_user is admin (Nexus)
    ~^GET:admin:.*:.*  http://10.35.0.100:8181;

    # If GET/HEAD/POST/PUT methods, host is gitlab.com, args contains "push", and remote_user is gitlab_custom_user
    ~^(GET|HEAD|POST|PUT):gitlab_custom_user:gitlab.com:.*push.*  https://gitlab.com:5043;

    # If GET/HEAD/POST methods, host is artifactory.com, and remote_user is empty
    ~^(GET|HEAD|POST|PUT)::artifactory.com.*  https://artifactory.com;

    # Default condition
    default http://10.35.0.100:8181;
}

server {
    listen 8080;
    resolver 10.10.110.20;

    location / {

        proxy_pass $docker_destination;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
       }
}
```

**Troubleshooting:**
- Enhance the nginx [log format](/devops/nginx/enhance-logging.md) and check if the traffic was forwarded to the correct upstream/ remote server.

## Use Case No: 2

❗ This use case is **NOT** recommended due to the modification of `/etc/hosts` but it is **ONLY** inteded to demonstrate different nginx and the client setup. ❗

- Nginx and Nexus are deployed as Docker containers.
- Pulling Docker images via Nginx Reverse Proxy from a remote **private** container registry.
- Pulling Docker image via Docker Proxy Instance (Nexus) from a remote **public/ private** container registry.
- **GOAL** is to cache Docker images on the Docker Proxy Instance (Nexus).

![Nginx Reverse Proxy](/devops/nginx/diagrams/nginx-reverse-proxy-2.png)

**NOTE**: `gitlab.com` is the my private container registry for the simplification

```
docker pull gitlab.com:5055/security-services/pre-commit:1.0
```

The following configuration has to be carried out:

> ❗ The goal is not to pull Docker images from GitLab directly but via Docker Proxy Intance (Nexus) using Nginx Reverse Proxy.
>
> ❗ When executing `docker pull gitlab.com:5055/security-services/pre-commit:1.0` on the GitLab Runner, the communication went directly to GitLab (bypassing Nexus) --> that is why the Nginx Reverse Proxy was deployed and `/etc/hosts` updated.

1. Modify `/etc/hosts` on the machine where Nginx resides where `gitlab.com` points to the `localhost`/ `127.0.0.1`.

```
127.0.0.1 gitlab.com
```

2. Create a new nginx configuration in `/etc/nginx/conf.d/reverse-proxy.conf`:

```
server {
    listen 5055;

    location / {

        proxy_pass http://docker-proxy-instance;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
       }
}
```

3. Docker Proxy Instance (Nexus) is setup with HTTP listeners - see [here](https://mtijhof.wordpress.com/2018/07/23/using-nexus-oss-as-a-proxy-cache-for-docker-images/).

4. Modify `/etc/hosts` on the GitLab Runner where the remote container registry `gitlab.com` points to Nginx Reverse Proxy:

```
10.35.0.26 gitlab.com
```

5. Configure GitLab Runner's configuration with `---engine-registry-mirrow` and `--engine-insecure-registry` that points to Nginx Reverse Proxy and Docker Proxy Instance (Nexus) accordingly.

### BEFORE using Nginx:

`docker pull gitlab.com:5055/security-services/pre-commit:1.0 --> Private Container Registry (gitlab.com)`

`docker pull alpine --> Public Docker Hub`

### AFTER using Nginx:

`docker pull gitlab.com:5055/security-services/pre-commit:1.0 --> Nginx Reverse Proxy --> Docker Proxy Instance (Nexus) --> Private Container Registry (gitlab.com)`

`docker pull alpine --> Docker Proxy Intance (Nexus) --> Public Docker Hub`

