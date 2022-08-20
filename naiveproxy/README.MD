##
```
ssh root@43.154.164.174
```

## Get this image
```
docker pull kpzhao/naiveproxy
```

## Modify the configuration
```
cat > /etc/naiveproxy/Caddyfile <<EOF
{
  servers {
    protocol {
      experimental_http3
    }
  }
}
:443, kpzhao.xyz
tls kaipengzhao@gmail.com
route {
        forward_proxy {
                basic_auth kpzhao 123456
                hide_ip
                hide_via
                probe_resistance
        }
        file_server {
                root /var/www/html
        }
}
EOF
```

#
## or use config files
```
docker run --network host --name naiveproxy -v ~/utiles/naiveproxy:/etc/naiveproxy -v /var/www/html:/var/www/html -v /var/log/caddy:/var/log/caddy -e PATH=/etc/naiveproxy/Caddyfile --restart=always -d kpzhao/naiveproxy
```
## client
```
{
  "listen": "socks://127.0.0.1:1080",
  "proxy": "quic://kpzhao:123456@kpzhao.xyz", # quic or http
  "log": ""
}
```
## bbr
### 修改系统变量
```
echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf && echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf
```
### 保存生效
```
sysctl -p
```
### 查看内核是否已开启BBR
```
sysctl net.ipv4.tcp_available_congestion_control
```
### 查看BBR是否启动
```
lsmod | grep bbr
```
## 后台运行
在程序目录下创建 ss-background.vbs
```
Set ws = CreateObject("Wscript.Shell")   
ws.run "naive.exe", vbhide
```
创建快捷方式放到 系统的启动栏中
以Win10为例，放到：

C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp

## linux
```
git clone https://github.com/kpzhao/config.git 
mkdir -p /etc/naiveproxy
cp ~/config/naiveproxy/naiveproxy /usr/bin/naiveproxy
cp ~/config/naiveproxy/config.json /etc/naiveproxy/config.json    
```
创建`/usr/lib/systemd/system/naiveproxy.service`

```
[Unit]
Description=naiveproxy Service
After=network-online.target

[Service]
Type=simple
User=nobody
ExecStart=/usr/bin/naiveproxy /etc/naiveproxy/config.json

[Install]
WantedBy=multi-user.target
```
