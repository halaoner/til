# Remove Docker images Without a Tag

```bash
docker rmi $(docker images -f "dangling=true" -q)
```
