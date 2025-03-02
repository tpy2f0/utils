## aria-pro
```
podman run -d \
    --name aria2-pro \
    --restart unless-stopped \
    --log-opt max-size=1m \
    --network host \
    -e PUID=$UID \
    -e PGID=$GID \
    -e RPC_SECRET=123456 \
    -e RPC_PORT=6800 \
    -e LISTEN_PORT=6888 \
    -v $PWD/aria2/config:/config \
    -v $PWD/aria2/downloads:/downloads \
    p3terx/aria2-pro
```
## ariang
```
docker run -d \
    --name ariang \
    --log-opt max-size=1m \
    --restart unless-stopped \
    -p 6880:6880 \
    p3terx/ariang
```
[aria2-pro](https://p3terx.com/archives/docker-aria2-pro.html)
