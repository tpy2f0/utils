`touch /$PWD/utils/filebrowser/filebrowser.db`

```
docker run \
    -v /root:/srv \
    -v /$PWD/utils/filebrowser/filebrowser.db:/database.db \
    -u $(id -u):$(id -g) \
    -p 8080:80 \
    filebrowser/filebrowser
```
