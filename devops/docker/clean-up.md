# Clean up (containers, images, volumes)

```bash
docker stop $(docker ps -a -q); docker rm $(docker ps -a -q); docker rmi -f $(docker images -aq); docker volume rm $(docker volume ls -q)
```
