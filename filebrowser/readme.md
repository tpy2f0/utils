`touch /$PWD/dotfile/filebrowser/filebrowser.db`
```
docker run -d \
    --name filebrowser \
    -v /root:/srv \
    -v /$PWD/dotfile/filebrowser/filebrowser.db:/database.db \
    --user $(id -u):$(id -g) \
    -p 8080:80 \
    --restart=always \
    filebrowser/filebrowser
```
