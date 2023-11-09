# Nginx Log Format

The default nginx log message format (`/etc/nginx/nginx.conf`) can be enhanced about additional parameters, for example, for better troubleshooting (to make sure that the forwarding rules work as expected) when using [nginx reverse proxy](https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/).

See [Nginx Reverse Proxy](/devops/nginx/proxy-forward.md) for the whole context.

Notice that `$docker_destination` in  `log_format` in the below `nginx.conf` that was added.

```
user  nginx;
worker_processes  auto;

error_log  /var/log/nginx/error.log notice;
pid        /var/run/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for" "$docker_destination"';

    access_log  /var/log/nginx/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  65;

    #gzip  on;

    include /etc/nginx/conf.d/*.conf;
}
```

Log message BEFORE enhancement of the nginx log format:

```
10.35.0.120 - - [09/Nov/2023:11:41:41 +0000] "PUT http://artifactory.com/v2/security-services/pre-commit/manifests/test HTTP/1.1" 201 0 "-" "docker/24.0.0 go/go1.20.4 git-commit/1331b8c kernel/5.15.0-1038-aws os/linux arch/amd64 UpstreamClient(Docker-Client/24.0.0 \x5C(linux\x5C))" "-"
```

Log message AFTER enhancement of the nginx logformat:


```
10.35.0.120 - - [09/Nov/2023:11:42:41 +0000] "PUT http://artifactory.com/v2/security-services/pre-commit/manifests/test HTTP/1.1" 201 0 "-" "docker/24.0.0 go/go1.20.4 git-commit/1331b8c kernel/5.15.0-1038-aws os/linux arch/amd64 UpstreamClient(Docker-Client/24.0.0 \x5C(linux\x5C))" "-" "https://artifactory.com"
```
