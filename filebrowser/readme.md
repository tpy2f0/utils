`touch /root/dotfile/filebrowser/filebrowser.db`
```
docker run -d \
    --name filebrowser \
    -v /root:/srv \
    -v /root/dotfile/filebrowser/filebrowser.db:/database.db \
    --user $(id -u):$(id -g) \
    -p 8080:80 \
    --restart=always \
    filebrowser/filebrowser
```
