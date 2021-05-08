```shell
docker build -t qemu-patch .
docker run -dit --network=host  qemu-patch
docker cp CONTAINER_ID:/root/qemu-patch ./
```
