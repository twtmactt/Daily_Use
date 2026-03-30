同步时间  
```dpkg-reconfigure tzdata```  
```
apt update
apt upgrade
apt install curl
apt install nano
```

修改配置文件  
```  
nano /usr/local/etc/xray/config.json
```
将以下内容粘贴并修改相应部分  
```  
{
    "log": {
        "loglevel": "warning"
    },
    "routing": {
        "domainStrategy": "IPIfNonMatch",
        "rules": [
            {
                "type": "field",
                "ip": [
                    "geoip:private"
                ],
                "outboundTag": "block"
            },
            {
                "type": "field",
                "protocol": [
                 "bittorrent"
                ],
                "ip": [
                    "geoip:cn"
                ],
                "outboundTag": "block"
            }
        ]
    },
    "inbounds": [
        {
            "listen": "0.0.0.0", #不要改
            "port": 1234,
            "protocol": "vmess",
            "settings": {
                "clients": [
                    {
                        "id": ""
                    }
                ]
            },
            "streamSettings": {
                "network": "tcp"
            }
        }
    ],
    "outbounds": [
        {
            "protocol": "freedom",
            "tag": "direct"
        },
        {
            "protocol": "blackhole",
            "tag": "block"
        }
    ]
}
```
启用v2ray
```
systemctl enable xray
systemctl start xray
```


开启端口
```
apt install firewalld
firewall-cmd --zone=public --add-port=端口/tcp --permanent    //永久将xxx端口加入开启规则
firewall-cmd --reload
```
开启bbr加速  
```
wget -N --no-check-certificate "https://raw.githubusercontent.com/dlxg/Linux-NetSpeed/master/tcp.sh" && chmod +x tcp.sh && ./tcp.sh
```
以下没用  
(for centos : systemctl enable v2ray)  
$sudo apt-get remove vim-common  
$sudo apt-get install vim


