# Lede或Openwrt路由器配置v2ray

#### 到https://github.com/v2ray/v2ray-core/releases下载v2ray-linux-arm.zip并解压，可通过以下命令压缩程序
```Shell
upx --lzma v2ray
upx --lzma v2ctl
```
#### 复制以下文件到相应的目录
```Shell
/usr/bin/v2ray/v2ray：V2Ray 程序；
/usr/bin/v2ray/v2ctl：V2Ray 工具；
/etc/v2ray/config.json：配置文件；
/usr/bin/v2ray/geoip.dat：IP 数据文件
/usr/bin/v2ray/geosite.dat：域名数据文件
```
#### 编辑 /etc/v2ray/config.json 文件来配置你需要的代理方式；
```json
{
  "log": {
    "loglevel": "warning"
  },
  "inbounds": [{
    "port": 1080,
    "listen": "0.0.0.0",
    "tag": "socks-inbound",
    "protocol": "socks",
    "settings": {
      "auth": "noauth",
      "udp": false,
      "ip": "127.0.0.1"
    },
    "sniffing": {
      "enabled": true,
      "destOverride": ["http", "tls"]
    }
  },
  {
    "port": 12345,
    "protocol": "dokodemo-door",
    "settings": {
      "network": "tcp,udp",
      "followRedirect": true
    },
    "sniffing": {
      "enabled": true,
      "destOverride": ["http", "tls"]
    }
  }],
  "outbounds": [
    {                                                        
      "tag": "direct",
      "protocol": "freedom",
      "streamSettings": {
        "sockopt": {
          "mark": 255
        }
      }
    },
    {
      "tag": "proxy",
      "protocol": "vmess",
      "settings": {
        "vnext": [
          {
            "address": "file.geniusy.com",
            "port": 443,
            "users": [
              {
                "id": "96458c94-2e5d-4d66-8c3f-317d22fa4c39",
                "alterId": 64,
                "security": "auto"
              }
            ]
          }
        ]
      },
      "streamSettings": {
        "network": "ws",
        "security": "tls",
        "tlsSettings": {
          "serverName": "file.geniusy.com",
          "allowInsecure": false
        },
        "wsSettings": {
          "path": "/video"
        },
        "sockopt": {
          "mark": 255
        }
      },
      "mux": {
        "enabled": true
      }
    },
    {
      "tag": "block",
      "protocol": "blackhole",
      "settings": {
        "response": {
          "type": "http"
        }
      }
    }
  ],
  "dns": {
    "servers": [
      "localhost",
      {
        "address": "8.8.8.8",
        "port": 53,
        "domains": [
          "geosite:google",
          "geosite:github",
          "geosite:netflix",
          "geosite:steam",
          "geosite:telegram",
          "geosite:tumblr",
          "geosite:bbc",
          "domain:googleapis.com",
          "domain:googleapis.cn",
          "domain:gstatic.com",
          "domain:ytimg.com",
          "domain:ggpht.com",
          "domain:youtube.com",
          "domain:googlevideo.com",
          "domain:gtv1.com",
          "domain:gtv2.com",
          "domain:google-analytics.com",
          "domain:googleanalytics.com",
          "domain:googlesyndication.com",
          "domain:googletagmanager.com",
          "domain:googletagservices.com",
          "domain:googleusercontent.com",
          "domain:wikipedia.org",
          "domain:dropbox.com",
          "domain:facebook.com",
          "domain:fbcdn.net",
          "domain:twitter.com",
          "domain:amazonaws.com",
          "domain:pornhub.com",
          "domain:sourceforge.net",
          "domain:ftchinese.com",
          "domain:textnow.com",
          "domain:twitch.tv",
          "domain:wikileaks.org",
          "domain:naver.com"
        ]
      }
    ]
  },
  "routing": {
    "domainStrategy": "IPIfNonMatch",
    "rules": [
      {
        "type": "field",
        "outboundTag": "direct",
        "domain": [
          "edu.cn",
          "gov.cn",
          "domain:geniusy.com",
          "domain:datainfinance.com",
          "domain:iqiyi.com",
          "domain:youku.com",
          "domain:bilibili.com",
          "domain:mgtv.com",
          "domain:le.com",
          "domain:sohu.com",
          "domain:baidu.com",
          "domain:qq.com",
          "domain:tencent.com",
          "domain:taobao.com",
          "domain:alipay.com",
          "domain:tmall.com",
          "domain:163.com",
          "domain:126.com",
          "domain:netease.com",
          "domain:douban.com",
          "domain:jd.com",
          "domain:12306.com",
          "domain:windows.com",
          "domain:microsoft.com",
          "domain:windowsupdate.com",
          "domain:live.com",
          "domain:outlook.com",
          "domain:hotmail.com",
          "domain:office.com",
          "domain:live.cn",
          "domain:apple.com",
          "domain:mzstatic.com",
          "domain:apple-mapkit.com",
          "domain:cdn-apple.com",
          "domain:cdn-apple.com.akadns.net",
          "domain:apple.com.edgekey.net",
          "domain:edgekey.net.globalredir.akadns.net",
          "domain:ls-apple.com.akadns.net",
          "domain:xiaomi.com",
          "domain:miui.com",
          "domain:mi.com",
          "domain:myendnoteweb.com",
          "domain:endnote.com",
          "domain:webofknowledge.com",
          "domain:incites.thomsonreuters.com",
          "domain:jstor.org",
          "domain:wiley.com",
          "domain:sciencedirect.com",
          "domain:springer.com",
          "domain:aaajournals.org",
          "domain:oup.com",
          "domain:cambridge.org",
          "domain:informs.org",
          "domain:ebscohost.com",
          "domain:proquest.umi.com",
          "domain:proquest.com",
          "domain:lexisnexis.com",
          "domain:emeraldinsight.com",
          "domain:sagepub.com",
          "domain:cnki.net",
          "domain:wanfangdata.com.cn",
          "domain:cqvip.com",
          "domain:tandfonline.com",
          "domain:heinonline.org",
          "domain:gtadata.com",
          "domain:resset.cn",
          "domain:cnrds.com",
          "domain:bvdinfo.com",
          "domain:bvdep.com",
          "domain:ceicdata.com"
	      ]
      },
      {
        "type": "field",        
        "outboundTag": "direct", 
        "ip": [
          "119.29.29.29",
          "223.5.5.5",
          "223.6.6.6",
          "61.139.2.69",
          "218.6.200.139",
          "202.98.96.68",
          "1.2.4.8",
          "210.2.4.8",
          "114.114.114.114",
          "114.114.115.115",
          "119.6.6.6",
          "35.220.143.216",
          "207.246.113.93",
          "geoip:cn",
          "geoip:private"
        ]                      
      },
      {
        "type": "field",
        "outboundTag": "proxy",
        "domain": [
          "geosite:google",
          "geosite:github",
          "geosite:netflix",
          "geosite:steam",
          "geosite:telegram",
          "geosite:tumblr",
          "geosite:bbc",
          "google.com",
          "domain:googleapis.com",
          "domain:googleapis.cn",
          "domain:gstatic.com",
          "domain:ytimg.com",
          "domain:ggpht.com",
          "domain:youtube.com",
          "domain:googlevideo.com",
          "domain:gtv1.com",
          "domain:gtv2.com",
          "domain:google-analytics.com",
          "domain:googleanalytics.com",
          "domain:googlesyndication.com",
          "domain:googleusercontent.com",
          "domain:wikipedia.org",
          "domain:dropbox.com",
          "domain:facebook.com",
          "domain:fbcdn.net",
          "domain:twitter.com",
          "domain:amazonaws.com",
          "domain:pornhub.com",
          "domain:sourceforge.net",
          "domain:ftchinese.com",
          "domain:textnow.com",
          "domain:twitch.tv",
          "domain:wikileaks.org",
          "domain:naver.com"
        ]                                      
      },                        
      {
        "type": "field",        
        "outboundTag": "proxy", 
        "ip": [
          "8.8.8.8",
          "8.8.4.4",
          "1.1.1.1",
          "9.9.9.9",
          "208.67.222.222",
          "208.67.220.220",
          "91.108.4.0/22",      
          "91.108.8.0/22",      
          "91.108.12.0/22",     
          "91.108.20.0/22",     
          "91.108.36.0/23",     
          "91.108.38.0/23",     
          "91.108.56.0/22",     
          "149.154.160.0/20",   
          "149.154.164.0/22",   
          "149.154.172.0/22",   
          "74.125.0.0/16",      
          "173.194.0.0/16",     
          "172.217.0.0/16",     
          "216.58.200.0/24",    
          "216.58.220.0/24"
        ]                      
      },
      {                                        
        "type": "field",                       
        "outboundTag": "block",                
        "domain": ["geosite:category-ads"]
      }                                       
    ]
  }
}
```

#### 新建/etc/init.d/v2ray文件以创建自启动任务
```Shell
START=90
USE_PROCD=1
start_service() {
  mkdir /var/log/v2ray > /dev/null 2>&1
  procd_open_instance
  procd_set_param respawn
  procd_set_param command /usr/bin/v2ray/v2ray -config /etc/v2ray/config.json
  procd_set_param file /etc/v2ray/config.json
  procd_set_param stdout 1
  procd_set_param stderr 1
  procd_set_param pidfile /var/run/v2ray.pid
  procd_close_instance
}
```
赋予启动脚本运行权限并设置自启动
```Shell
chmod +x v2ray
service v2ray enable
```

#### 测试并运行v2ray
```Shell
service v2ray start
```
可通过以下命令检查代理是否连通：
```Shell
curl -x socks5://127.0.0.1:1080 google.com
```
若返回以下内容则表示代理设置没问题
```html
<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
<TITLE>301 Moved</TITLE></HEAD><BODY>
<H1>301 Moved</H1>
The document has moved
<A HREF="http://www.google.com/">here</A>.
</BODY></HTML>
```

#### 在网关的配置，添加dokodemo door协议的入站配置 ，并开启sniffing；还要在所有outbound的streamSettins添加SO_MARK。配置形如（配置中的...代表原来客户端的通常配置）,本段配置已整合进上面的配置文件中：
```json
{
"routing": {...},
"inbounds": [
 {
   ...
 },
 {
   "port": 12345, //开放的端口号
   "protocol": "dokodemo-door",
   "settings": {
     "network": "tcp,udp",
     "followRedirect": true // 这里要为 true 才能接受来自 iptables 的流量
   },
   "sniffing": {
     "enabled": true,
     "destOverride": ["http", "tls"]
   }
 }
],
"outbounds": [
 {
   ...
   "streamSettings": {
     ...
     "sockopt": {
       "mark": 255  //这里是 SO_MARK，用于 iptables 识别，每个 outbound 都要配置；255可以改成其他数值，但要与下面的 iptables 规则对应；如果有多个 outbound，最好奖所有 outbound 的 SO_MARK 都设置成一样的数值
     }
   }
 }
 ...
]
}
```

#### 设定 TCP 透明代理的 iptables 规则，命令如下
```Shell
iptables -t nat -N V2RAY # 新建一个名为 V2RAY 的链
iptables -t nat -A V2RAY -d 192.168.0.0/16 -j RETURN # 直连 192.168.0.0/16 
iptables -t nat -A V2RAY -p tcp -j RETURN -m mark --mark 0xff # 直连 SO_MARK 为 0xff 的流量(0xff 是 16 进制数，数值上等同与上面配置的 255)，此规则目的是避免代理本机(网关)流量出现回环问题
iptables -t nat -A V2RAY -p tcp -j REDIRECT --to-ports 12345 # 其余流量转发到 12345 端口（即 V2Ray）
iptables -t nat -A PREROUTING -p tcp -j V2RAY # 对局域网其他设备进行透明代理
iptables -t nat -A OUTPUT -p tcp -j V2RAY # 对本机进行透明代理
```
然后设定 UDP 流量透明代理的 iptables 规则，命令如下
```Shell
ip rule add fwmark 1 table 100
ip route add local 0.0.0.0/0 dev lo table 100
iptables -t mangle -N V2RAY_MASK
iptables -t mangle -A V2RAY_MASK -d 192.168.0.0/16 -j RETURN
iptables -t mangle -A V2RAY_MASK -p udp -j TPROXY --on-port 12345 --tproxy-mark 1
iptables -t mangle -A PREROUTING -p udp -j V2RAY_MASK
```
去掉注释整合版
```Shell
iptables -t nat -N V2RAY
iptables -t nat -A V2RAY -d 192.168.0.0/16 -j RETURN
iptables -t nat -A V2RAY -p tcp -j RETURN -m mark --mark 0xff
iptables -t nat -A V2RAY -p tcp -j REDIRECT --to-ports 12345
iptables -t nat -A PREROUTING -p tcp -j V2RAY
iptables -t nat -A OUTPUT -p tcp -j V2RAY
ip rule add fwmark 1 table 100
ip route add local 0.0.0.0/0 dev lo table 100
iptables -t mangle -N V2RAY_MASK
iptables -t mangle -A V2RAY_MASK -d 192.168.0.0/16 -j RETURN
iptables -t mangle -A V2RAY_MASK -p udp -j TPROXY --on-port 12345 --tproxy-mark 1
iptables -t mangle -A PREROUTING -p udp -j V2RAY_MASK
```
v2ray官方原版iptables
```shell
# Create new chain
iptables -t nat -N V2RAY
iptables -t mangle -N V2RAY
iptables -t mangle -N V2RAY_MARK

# Ignore your V2Ray server's addresses
# It's very IMPORTANT, just be careful.
iptables -t nat -A V2RAY -d 123.123.123.123 -j RETURN

# Ignore LANs and any other addresses you'd like to bypass the proxy
# See Wikipedia and RFC5735 for full list of reserved networks.
iptables -t nat -A V2RAY -d 0.0.0.0/8 -j RETURN
iptables -t nat -A V2RAY -d 10.0.0.0/8 -j RETURN
iptables -t nat -A V2RAY -d 127.0.0.0/8 -j RETURN
iptables -t nat -A V2RAY -d 169.254.0.0/16 -j RETURN
iptables -t nat -A V2RAY -d 172.16.0.0/12 -j RETURN
iptables -t nat -A V2RAY -d 192.168.0.0/16 -j RETURN
iptables -t nat -A V2RAY -d 224.0.0.0/4 -j RETURN
iptables -t nat -A V2RAY -d 240.0.0.0/4 -j RETURN

# Anything else should be redirected to Dokodemo-door's local port
iptables -t nat -A V2RAY -p tcp -j REDIRECT --to-ports 12345

# Add any UDP rules
ip route add local default dev lo table 100
ip rule add fwmark 1 lookup 100
iptables -t mangle -A V2RAY -p udp --dport 53 -j TPROXY --on-port 12345 --tproxy-mark 0x01/0x01
iptables -t mangle -A V2RAY_MARK -p udp --dport 53 -j MARK --set-mark 1

# Apply the rules
iptables -t nat -A OUTPUT -p tcp -j V2RAY
iptables -t mangle -A PREROUTING -j V2RAY
iptables -t mangle -A OUTPUT -j V2RAY_MARK
```

本人测试可用版本，仅开启TCP
```Shell
# Create new chain
iptables -t nat -N V2RAY

# Ignore your V2Ray server's addresses
# It's very IMPORTANT, just be careful.
# Change 123.123.123.123 to your server ip
iptables -t nat -A V2RAY -d 123.123.123.123 -j RETURN
iptables -t nat -A V2RAY -p tcp -j RETURN -m mark --mark 0xff

# Ignore LANs and any other addresses you'd like to bypass the proxy
# See Wikipedia and RFC5735 for full list of reserved networks.
iptables -t nat -A V2RAY -d 0.0.0.0/8 -j RETURN
iptables -t nat -A V2RAY -d 10.0.0.0/8 -j RETURN
iptables -t nat -A V2RAY -d 127.0.0.0/8 -j RETURN
iptables -t nat -A V2RAY -d 169.254.0.0/16 -j RETURN
iptables -t nat -A V2RAY -d 172.16.0.0/12 -j RETURN
iptables -t nat -A V2RAY -d 192.168.0.0/16 -j RETURN
iptables -t nat -A V2RAY -d 224.0.0.0/4 -j RETURN
iptables -t nat -A V2RAY -d 240.0.0.0/4 -j RETURN

# Anything else should be redirected to Dokodemo-door's local port
iptables -t nat -A V2RAY -p tcp -j REDIRECT --to-ports 12345

# Apply the rules
iptables -t nat -A PREROUTING -p tcp -j V2RAY
```

iptables若提示“unknown option "--on-port"”，则运行以下命令安装缺失包
```shell
opkg install iptables-mod-tproxy # 必装
# 以下包尽量安装
ip-tiny / ip-full
ipset
iptables
kmod-ipt-ipset
kmod-ipt-tproxy
libipset
```
