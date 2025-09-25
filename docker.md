# Docker

## log into a container to check a package version

For example, to check the `linux-libc-dev` package version

```bash
docker ps
docker exec -it <admin container id from docker ps> sh
dpkg -l linux-libc-dev
```
