## 文件名：mcjava联机.toml
```
#服务器ip
serverAddr = "47.108.85.41"
#frp端口
serverPort = 7000
#授权方法
auth.method = "token"
#授权令牌
auth.token = "token123456"
#以上部分不要随便动

[[proxies]]
#名称自定义即可
name = "minecraft"
#协议类型一般为tcp或udp
type = "tcp"
#保持127.0.0.1或localhost
localIP = "127.0.0.1"
#内网端口 看你要映射的项目是什么端口
localPort = 25565
#外网端口 这个自定 范围在6000~7000 或 25565 和19132（这两个个是minecraft java和be版的默认端口）
remotePort = 25565

[[proxies]]
##名称自定义即可
name = "bluemap"
超文本协议
type = "http"
localIP = "127.0.0.1"
localPort = 8100
#域名
customDomains = ["bluemap.youzhidanbairu.cloudns.biz"]
```
推荐客户端：[FRPmgr](https://github.com/koho/frpmgr/releases/tag/v1.19.2)