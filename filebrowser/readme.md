`touch /$PWD/config/filebrowser/filebrowser.db`
```
docker run -d \
    --name filebrowser \
    -v /root:/srv \
    -v /$PWD/config/filebrowser/filebrowser.db:/database.db \
    --user $(id -u):$(id -g) \
    -p 8080:80 \
    --restart=always \
    filebrowser/filebrowser
```
