`touch /$PWD/utils/filebrowser/filebrowser.db`

```
docker run \
    -v /root:/srv \
    -v /$PWD/utils/filebrowser/filebrowser.db:/database.db \
    -e PUID=$(id -u) \
    -e PGID=$(id -g) \
    -p 8080:80 \
    filebrowser/filebrowser:s6
```
