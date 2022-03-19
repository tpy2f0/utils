```
sudo docker run -d \
  --restart=always \
  -v /etc/alist:/opt/alist/data \
  -p 5244:5244 \
  --name="alist" \
  xhofe/alist:latest
```
[alist doc](https://alist-doc.nn.ci/docs/install/docker)
